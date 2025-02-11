# CAW (Compact Adaptive Word) Protocol

CAW is a lightweight session layer (OSI 5) protocol designed for low-bandwidth communication. Its innovative approach to word definitions and checksum-based dialect negotiation enables brief and context-dependent messaging.  

Because it implements the minimum required data integrity features (checksum), it can be used for OSI layers 3-5 where link-sharing is not required. We intend to release purpose-built complementary protocols for layer 3 and layer 4 to work with CAW with significantly lower overhead than current IP + UDP/TCP stacks, while preserving compatibility with IP + UDP/TCP.  

---
Defining Features

 - Ultra-compact size: CAW messages are extremely concise, making them ideal for low-bandwidth communication channels.
 - Dynamic word definitions: Word meanings are context-dependent and unbound by the specification of the protocol, significantly reducing packet size.
 - Checksum-based dialect negotiation: Senders and receivers must negotiate the dialect before messages can be understood. A onetime traffic tradeoff for sustainably smaller packets.

How CAW Works

 - Dialect negotiation: The sender and receiver agree on a dialect by exchanging checksums. This ensures that both parties are using the same word definitions.
 - Message construction: The sender constructs a message using the negotiated dialect. Word meanings are inferred from the context, reducing the need for explicit definitions.
 - Message transmission: The message is transmitted to the receiver.
 - Message interpretation: The receiver interprets the message using the negotiated dialect and context.

Benefits

 - Low bandwidth usage: CAW's compact messages reduce bandwidth usage, making it ideal for UAV communication.
 - Increased flexibility: Dynamic word definitions enable the protocol to adapt to changing situations and contexts.

Implementation

CAW is designed to be implemented in a variety of programming languages. The protocol's compact size and simplicity make it an ideal choice for resource-constrained UAV systems. Protocol specifications and reference implementations will be added to this repository.  

License

CAW is licensed under the Mozilla Public License, version 2.0 (MPL-2.0). See the [LICENSE](LICENSE) file for more information.
