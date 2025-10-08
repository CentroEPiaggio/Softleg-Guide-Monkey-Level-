# SOFTLEG — Setup Guide

## 1. Launch the Interface

1. Connect to the Wi-Fi network:  
   **SSID:** `softleg_wifi`  
   **Password:** `1234567890`

2. Open a terminal and connect via SSH:
   ```bash
   ssh mulsbc@192.168.88.1
   ```
   **Password:** `123456`

3. Switch to superuser:
   ```bash
   sudo su
   ```
   **Password:** `123456`

---

## 2. Restart Chrony Service

```bash
sudo systemctl restart chrony.service
```

---

## 3. Set Up the ROS Environment

```bash
cd mulsbc_ws/
source /opt/ros/humble/setup.bash
source install/setup.bash
export ROS_DOMAIN_ID=13
```

---

## 4. Check Chrony Synchronization

```bash
chronyc sources
```

If there is **no asterisk (`*`)** next to a source, it means synchronization is not active.  
To fix this:

1. Search for **CHRONY** settings:
   ```bash
   Ctrl + R
   ```
   Type: `chrony`

2. Edit the Chrony configuration file:
   ```bash
   sudo nano /etc/chrony/chrony.conf
   ```

3. **Modify the network** according to the output of `ip a`.  
   Make sure you do this **on both terminals** (the `mulsbc` one is the Raspberry Pi).  
   > On the Raspberry Pi, **omit the “/..”** part.

4. Restart the Chrony service:
   ```bash
   sudo systemctl restart chrony.service
   ```

✅ **Chrony setup complete.**

---

## 5. Launch the MJBots Interface

```bash
ros2 launch pi3hat_hw_interface start_MJBots_Pi3Hat_hw_Interface.launch.py urdf_file:=softleg_jump.urdf.xacro conf_file:=2D_Leg.yaml
```

---

## 6. Shutdown Raspberry Pi

```bash
sudo shutdown now
```

---

# 🧪 FATIGUE TEST SETUP

Open a **new terminal** on your local machine:

```bash
cd <your_workspace>
source /opt/ros/humble/setup.bash
source install/setup.bash
export ROS_DOMAIN_ID=13

ros2 launch fatigue_test launch_fatigue_test.py
```

---

# 📊 PLOTJUGGLER VISUALIZATION

Open **another terminal**:

```bash
cd <your_workspace>
source /opt/ros/humble/setup.bash
source install/setup.bash
export ROS_DOMAIN_ID=13

ros2 run plotjuggler plotjuggler
```

---

# 🎥 Q-ANALYSIS (QUALISYS) — “SCIMMIA” GUIDE

## 1. Network Setup

- Connect via **Ethernet** to the **“Vicone”** network through the switch.  
- If the **camera** doesn’t connect, **unplug and reconnect** its power cable.

---

## 2. Launch the Qualisys Driver

```bash
cd <your_workspace>
source /opt/ros/humble/setup.bash
source install/setup.bash
export ROS_DOMAIN_ID=13

ros2 launch qualisys_driver qualisys.launch.py
```

---

## 3. Visualize in PlotJuggler

- Open **PlotJuggler**
- Select the topic: `/Rgod Bodies`
- The body of interest is **Body 7**