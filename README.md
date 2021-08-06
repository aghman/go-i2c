I2C-bus go module to handle interaction with sensors and other devices on Raspberry Pis 
==============================================================================================

[![Go Report Card](https://goreportcard.com/badge/github.com/aghman/go-i2c)](https://goreportcard.com/report/github.com/aghman/go-i2c)
[![GoDoc](https://godoc.org/github.com/aghman/go-i2c?status.svg)](https://godoc.org/github.com/aghman/go-i2c)
[![MIT License](http://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

This library written in [Go programming language](https://golang.org/) intended to activate and interact with the I2C bus by reading and writing data.

Compatibility
-------------

TBD.

Golang usage
------------

```go
func main() {
  // Create new connection to I2C bus on 2 line with address 0x27
  i2c, err := i2c.NewI2C(0x27, 2)
  if err != nil { log.Fatal(err) }
  // Free I2C connection on exit
  defer i2c.Close()
  ....
  // Here goes code specific for sending and reading data
  // to and from device connected via I2C bus, like:
  _, err := i2c.Write([]byte{0x1, 0xF3})
  if err != nil { log.Fatal(err) }
  ....
}
```

Getting help
------------

GoDoc [documentation](http://godoc.org/github.com/aghman/go-i2c)

Troubleshooting
--------------

- *How to enable I2C bus on a Raspberry Pi:*
Run 'sudo raspi-config' to activate I2C bus.
Go to "Interfacing Options" menu, to active I2C bus.
After configuration is complete, you should have device /dev/i2c-1 present.

- *How to find I2C bus allocation and device address:*
Use i2cdetect command-line utility "i2cdetect -y X", where X may vary from 0 to 5 or more,
to discover address occupied by peripheral device. To install utility you should run
`apt install i2c-tools` on debian-kind system. `i2cdetect -y 1` sample output:
	```
	     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
	00:          -- -- -- -- -- -- -- -- -- -- -- -- --
	10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
	70: -- -- -- -- -- -- 76 --    
	```

License
-------

Go-i2c is licensed under MIT License.
