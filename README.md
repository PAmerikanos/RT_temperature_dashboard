# RT_temperature_dashboard
Dashboard to monitor temperature readings from IoT sensor in real time.

## Setup
1. Configure I2C: `raspi-config > Interface Options > I2C > Enable`
2. Add to `/boot/firmware/config.txt`:
    ```
    dtparam=i2c_arm=on
    i2c_arm_baudrate=9600
    ```
3. Install dependencies: 
    ```
    sudo apt-get update
    sudo apt-get install python-pip
    sudo apt-get install libatlas-base-dev
    sudo pip3 install mcp9600
    sudo pip3 install matplotlib
    ```
4. Clone Git repo: `git clone https://github.com/PAmerikanos/RT_temperature_dashboard.git`

## Operation
1. Turn RPi on and connect it to the Internet. Automatic WiFi connection is set to `Pefki` SSID.
2. On computer within the LAN:
    1. Log into router to find RPi's IP address.
    2. In one terminal record temperature in realtime to `temperature.log` (every run overwrites the last one):
        1. Connect to RPi using SSH: `ssh pi@192.168.1.XXX` / `pass: 0000`
        2. `cd RT_temperature_dashboard`
        3. `source ~/venv/default/bin/activate`
        4. `nohup python3 log_temp.py &`
    3. In a separate terminal run the Flask server:
        1. Connect to RPi using SSH: `ssh pi@192.168.1.XXX` / `pass: 0000`
        2. `cd RT_temperature_dashboard`
        3. `source ~/venv/default/bin/activate`
        4. `nohup python3 run_flask.py &`

    `Nohup` allows the recording & serving to continue even if WiFi or SSH connection is lost.
    - `tail -f nohup.out` to monitor progress/nohup's output.
    - `kill <PID>` to kill either process.
3. On client device open browser at `http://192.168.1.XXX:5000/`

## References
- https://www.pi-shop.ch/thermocouple-amplifier-breakout
- https://github.com/pimoroni/mcp9600-python
