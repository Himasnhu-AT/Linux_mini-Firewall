# Mini Firewall Application

This is a mini firewall application implemented in C. It allows users to add, delete, and print firewall rules based on specific criteria such as source IP, destination IP, source port, and more.

## Usage

To use the mini firewall application, you can run the compiled executable with different command-line options. Here are the available options:

```batch
mf [-a <action>] [-c <protocol>] [-d <rule_number>] [-h] [--in] [-m <src_netmask>]
[-n <dest_netmask>] [--out] [-o] [-p <src_port>] [-q <dest_port>] [-s <src_ip>] [-t <dest_ip>]
```

- `-a <action>`: Specify the rule action (BLOCK or LOG).
- `-c <protocol>`: Specify the protocol of the packet to operate (1 for TCP, 2 for UDP, 3 for both).
- `-d <rule_number>`: Delete a specified rule using the rule number.
- `-h`: Print the usage of the mini firewall application.
- `--in`: Specify the in-packet to operate.
- `-m <src_netmask>`: Specify the netmask length of the source packet to operate.
- `-n <dest_netmask>`: Specify the netmask length of the destination packet to operate.
- `--out`: Specify the out-packet to operate.
- `-o`: Print the specified rules.
- `-p <src_port>`: Specify the source port of the packet to operate.
- `-q <dest_port>`: Specify the destination port of the packet to operate.
- `-s <src_ip>`: Specify the source IP of the packet to operate.
- `-t <dest_ip>`: Specify the destination IP of the packet to operate.

Example: `sudo ./mf -a BLOCK --in -t 31.13.87.36 -n 24`

## Compilation

To compile the mini firewall application, use a C compiler (such as gcc) with the following command:

```batch
gcc -o mf mf.c
```

## Working

The mini firewall application uses a command-line interface (CLI) to interact with the user and perform firewall operations. Here's how the code works:

1. The code defines a `mf_rule` structure to represent a firewall rule. Each rule contains properties such as source IP, destination IP, source port, destination port, action, and more.

2. The code defines functions to convert IP addresses between string and host long formats and to print or send firewall rules.

3. The `main` function parses the command-line options provided by the user using the `getopt_long` function. Based on the options, the code performs the corresponding actions, such as adding, deleting, or printing firewall rules.

4. When adding a rule, the code initializes a `mf_rule` object and sets its properties based on the provided command-line options. It then sends the rule to the mini firewall by writing it to the `/proc/miniFirewall` file.

5. When printing rules, the code reads the rules from the `/proc/miniFirewall` file and displays them on the console by calling the `print_a_rule` function.

6. When deleting a rule, the code reads the rule number from the command-line options and sends it to the mini firewall by writing it to the `/proc/miniFirewall` file.

7. The code also includes a `usage` function that prints the usage information for the mini firewall application.

## License

This mini firewall application is licensed under the [MIT License](LICENSE).