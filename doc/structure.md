# Structure of CAW

Definitions:
 - _dialect_ - A specific implementation of CAW containing a schema of features and modules. Dialects can be completely original, or denoted as derivative of a more common one.
 - _schema_ - The structure and format of a CAW dialect.

## Very High Level Overview:
There are two object types in CAW: modules and features.

Features are where the power and efficiency of CAW lies. They are at their most fundamental, an address with an optional data field. Typically, "features" are used for triggering functions or updating or retrieving values, however, they can also be used in more creative and complex ways. You could easily implement a data channel inside of a feature, or implement TCP-like packet counters. Features can implement methods, ideally in the first byte of the data field, while modules cannot.

Modules give CAW its extensibility and modularity, they're also more opinionated than features. They act act as a container for features and other modules, can have default behaviors or values, and must implement specific capabilities defined by the CAW specification.

Every dialect of CAW has at least 2 modules, the "root" module, and a reserved "definition" module which always exists at address  0x00.

The "magic" of CAW is in the 0x00 byte and the module that exists beneath it. This address is reserved in every module and implements the "definition" module for its parent.

The "definition" module is a special module that itself contains modules and features, for this module the location, data type, packet size, and so on are all prescribed by the CAW protocol. These include:

 Feature 0* - NULL: The ID of the module dialect. This is a sha256sum of the schema of the parent module and all of its children.
  - Method 1
 Feature 1 - The name of the module. (optional) ISO-8859-1. (ASCII, 7 bit characters)
 Feature 2* - The schema. Transfer method TBD.
 Feature 3 - The "like" ID. This is the ID of another dialect the current dialect is derived from. This is optional, but can significantly reduce the overhead of the protocol negotiation process.
 Feature 4 - URL that can be used to download the module's schema, this can be non web paths as well following the URL format, e.g. file:///home/user/schema.caw
 Feature 5 - Array of neighbors that may have the schema, first a byte for length of the array, then... (for fetching from a higher bandwidth source). format is [s|4|6] (for serial, ipv4, or ipv6) : then the address. Semi colons delimit the array object end. E.g.
 - "14:192.168.1.1:8080" where 1 is the number of items in the array, 4 is for ipv4, and 192.168.1.1:8080 is the ipv4 + port of the neighbor.

 Feature 10 - Enable or disable packet size prefix.
 Feature 11 - Enable or disable packet CRC.


## Notes:

1. CAW DOES NOT IMPLEMENT ROUTING AND NEVER WILL. You should wrap CAW packets in a lower level protocol designed for that if you need it. We recommend UDP.
2. Caw will probably not implement addressing either. But this can be part of a dialect.
