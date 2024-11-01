# Wavin Sentio Connect

Welcome to **Wavin Sentio Connect** – a user-friendly, event-driven Python library designed to simplify the interaction with Wavin Sentio in an event-driven way.

## Getting Started

1. **Installation**: Install the library using pip.
    ```bash
    pip install wavin-sentio-connect
    ```
2. **Basic Usage**: Define your DataPointKeys to a Modbus device with minimal code.
    ```python
    from collections.abc import Callable
    from src.wavin_sentio_connect import *

    class MyDatapointKey(ModbusDatapointKey):
        MAJOR_VERSION = "major_version"
        
    class MySetpointKey(ModbusSetpointKey):
        MY_SETPOINT = "my_setpoint"

    class MyModbusDevice(ModbusDeviceBase):
        def __init__(self, device_info: ModbusDeviceInfo):
            super().__init__(device_info)

            self._attr_manufacturer="<manufacturer>"
            self._attr_model_name="<model_name>"
            self._attr_datapoints = [
                ModbusDatapoint(key=MyDatapointKey.MAJOR_VERSION, read_address=1, divider=1, signed=True),
            ]
            self._attr_setpoints = [
                ModbusSetpoint(key=MySetpointKey.MY_SETPOINT, read_address=1, write_address=1 ,divider=1, min=1, max=10, signed=True),
            ]

    class MyModbusDeviceAdapter(ModbusDeviceAdapter):

        def _translate_to_model(self, device_info: ModbusDeviceInfo) -> Callable[[ModbusDeviceInfo], ModbusDevice]|None: 
            return MyModbusDevice

    class MyModbusTCPEventConnect(ModbusTCPEventConnect):
        _attr_adapter = MyModbusDeviceAdapter()
    ```

## Documentation
### Client Capabilities

The Wavin Sentio Connect offers a range of methods to facilitate seamless interaction with Modbus devices. Key features include:

- **Subscribe**: Easily subscribe to data points and receive updates.
- **Unsubscribe**: Manage your subscriptions effortlessly.
- **Comprehensive Methods**: A variety of methods to handle different Modbus operations.

Let the Event Connect handle the communication, allowing you to focus on responding to changes and managing your Modbus devices efficiently.

## Disclaimer

Wavin Sentio Connect is provided "as is", without warranty of any kind. The authors and contributors are not responsible for any damage or data loss that may occur from using this library. Users are solely responsible for ensuring the proper and safe operation of their Modbus devices.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

