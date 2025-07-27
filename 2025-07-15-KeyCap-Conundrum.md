

**Challenge Description**

A USB keyboard was used to type a secret message, leaving behind a trace in the form of a USB pcap file. Your task is to analyze the packet data, reconstruct the keystrokes, and uncover the hidden flag. Can you decode the captured data and retrieve the secret?


**Understanding How a USB Keyboard Works**

A **USB keyboard** is a standard computer keyboard that connects to a computer using a Universal Serial Bus **(USB)** interface instead of older ports like PS/2. When you type on a USB keyboard,  keystrokes are sent as digital signals over the USB connection, and these can be intercepted or recorded by tools designed to monitor USB traffic.

When a key is pressed on a USB keyboard, a sequence of events occurs that ultimately results in the character being displayed or action being performed on the computer. First, the key press generates a keystroke event that is detected by the keyboard’s internal microcontroller. This microcontroller translates the pressed key into a specific code known as a USB HID (Human Interface Device) keycode, which uniquely represents the key. This keycode is then packaged into a small USB packet typically 8 bytes long and sent to the host computer using an interrupt transfer method over the USB connection. Once the host receives the packet, the operating system interprets the keycode and takes the appropriate action, such as displaying a character on the screen or executing a command. This entire process happens rapidly and continuously as the user types.

**How It Leaves a Digital Traces**

When USB traffic is captured for example, during forensic analysis, debugging, or cybersecurity investigations every packet sent from a USB keyboard to the computer is logged. These packets include what is known as an HID (Human Interface Device) report, which is typically 8 bytes in length. Each report contains important information such as whether any modifier keys (like Shift, Ctrl, or Alt) were held down and up to six simultaneous keypresses. For instance, a packet with the hexadecimal sequence `00 00 04 00 00 00 00 00` indicates that the user pressed the letter 'a' (since `0x04` corresponds to 'a' in the USB HID standard), while `02 00 04 00 00 00 00 00` indicates that the user pressed Shift and 'a' together, which produces a capital 'A'. Because each key press is translated into a structured USB packet, it becomes possible to reconstruct everything the user typed by analyzing the captured packet data.
