# RT_temperature_dashboard - Under development
Dashboard to monitor temperature readings from IoT sensor in real time.

To run:
1. Open terminal and initialize Bokeh server: `bokeh serve test.py --allow-websocket-origin localhost:5006 --allow-websocket-origin 192.168.1.7:5006 --allow-websocket-origin 192.168.1.2:5006 --show`
2. Open browser at `http://localhost:5006/test` or `192.168.1.XXX:5006`
