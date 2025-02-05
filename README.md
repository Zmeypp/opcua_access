# OPC UA Client Library

You can install the library via command :

```
pip install opc-full-connect
```

## Overview

This library provides functionality for connecting to OPC UA servers. It requires OpenSSL for cryptographic operations.

**Note:** This library has been tested only on Windows.

## Prerequisites

Before using this library, you need to install OpenSSL and set up your project directory as follows:

```
root/
├── openssl/
│ └── bin/openssl.exe
└── main.py
```



### Installing OpenSSL on Windows

1. Download the OpenSSL installer for Windows from [the official OpenSSL website](https://www.openssl.org/).
2. Install OpenSSL and ensure that `openssl.exe` is placed in the `openssl/bin/` directory of your project.
3. Ensure that your `openssl` directory is properly set up according to the structure mentioned above.

## Usage

To use this library, you need to set up your `main.py` file as follows:

```python
import asyncio
from opc_full_connect import create_cert, OPCUAClient

async def main():

    # Create the certificate for OPC connexion

    certificate_folder_name = "certificates"
    configuration_name = "cert_conf"
    private_key_name = "pk"
    certificate_name = "cert"

    create_cert(
        certificate_folder_name,
        configuration_name,
        private_key_name,
        certificate_name
    )

    opc_url = "your_url"
    opc_username = "username"
    opc_password = "password"
    opc_policy = "policy"
    opc_mode = "mode"
    opc_certificate_path = "cert_path"
    opc_private_key_path = "pk_path"
    opc_application_uri = "urn:freeopcua:client"

    # Create an instance of OPCUAClient
    client_instance = OPCUAClient(opc_url,
                                  opc_policy,
                                  opc_mode,
                                  opc_certificate_path,
                                  opc_private_key_path,
                                  opc_username,
                                  opc_password,
                                  opc_application_uri
                                )

    # Connect to the OPC UA server
    await client_instance.connect_to_opc()

    # ID of the node to retrieve the value from
    node_id = "ns=2;s=2"

    # Retrieve the value of the node
    try:
        node_value = await client_instance.get_node_value(node_id)
        print(f"Value of node {node_id}: {node_value}")
    except Exception as e:
        print(f"Error retrieving node value: {e}")

# Run the main asynchronous function
if __name__ == "__main__":
    asyncio.run(main())
```

### License
This library is licensed under the MIT License. Please refer to the LICENSE file for more details.

### Support
For issues or questions, please open an issue on GitHub.

### Acknowledgements
This library uses OpenSSL for cryptographic functions. Please refer to the OpenSSL website for more information.
