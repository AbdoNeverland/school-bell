# SchoolBell (جرس المؤسسة)
Modernizing school infrastructure doesn't always require expensive industrial equipment. This tutorial explains how to transform a standard Android smartphone into a dedicated "Android Server" to manage a smart school bell system.

By leveraging Tuya smart sockets and a custom mobile application, you can automate school periods, manage seasonal schedules like Ramadan or Summer time, and even automate the server's own power management to protect its battery—all through a localized, cost-effective setup.


🛠️ Requirements
Android Server: An Android phone to act as the "brain" (Hotspot + Controller).

Tuya Smart Socket: A dual-switch model (Switch 1 for the bell, Switch 2 for the phone charger).

Electric Bell: Connected to the socket.

Personal Phone: For initial Tuya setup.

PC/Laptop: To extract the local "Device Key" using Python.

School Bell App: Installed on the Android Server.

📝 Step-by-Step Implementation
Phase 1: Network Configuration
The goal is to make the socket "think" the Android Server is a home Wi-Fi router.

On the Android Server, go to settings and enable the Mobile Hotspot.

Set a simple SSID (Network Name) and Password.

Connect your Personal Phone to this hotspot.

Phase 2: Tuya Device Pairing
Plug the socket into a power outlet. Ensure the light is blinking rapidly (Pairing Mode).

Open the Tuya Smart or Smart Life app on your Personal Phone.

Add the device. When asked for Wi-Fi details, enter the SSID and Password of the Android Server's hotspot.

Once paired, the socket is now "talking" to the Android Server.

Phase 3: Extracting the Local Key (The "PC" Part)
Tuya devices require a "Local Key" for offline control without using the cloud.

On your PC: Install Python and the TinyTuya library:
pip install tinytuya

Tuya IoT Platform:

Create an account at iot.tuya.com.

Create a Cloud Project and link it to your Tuya App account (via the "Link Tuya App Account" tab).

In Devices, copy your Device ID.

In Service API, copy your Access ID (API Key) and Access Secret.

Run the Wizard: Open your terminal/command prompt and run:
python -m tinytuya wizard

Follow the prompts to enter your API credentials. It will output a list of devices—copy the "Local Key" for your socket.

Phase 4: Setting up the School Bell App
Open the School Bell App on the Android Server.

Enter the Device ID and the Local Key (Password) you just found.

Tap Search for IP (Ensure the Hotspot is active). The app will find the socket's local address on the hotspot network.

Test: Press the On/Off buttons in the app. You should hear the socket click.

⚡ Hardware Integration & Features
Wiring the System
Switch 1: Plug the Electric Bell here. This will handle the ringing schedules.

Switch 2: Plug the Android Server's Charger here.

Smart Battery Management
The app acts as a Battery Management System.

Logic: When the phone’s battery drops (e.g., below 60%), the app sends a command to Switch 2 to turn ON. Once it reaches 75%, it turns OFF. This prevents battery swelling and extends the life of your "server."

Scheduling Options
You can configure the ringing patterns for different seasonal needs:

Winter/Summer Time: Standard school hours.

Ramadan Mode: Reduced hours or shifted schedules.

[!CAUTION]
Important Note: If you re-pair the socket to a different phone or reset it, the Local Key will change. You will need to run the TinyTuya wizard again to get the new key.
