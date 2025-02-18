# **Solution When you facing, how to connect EC2 instance with MobaXterm**
---

## **Step 1: Ensure You Are Using the Correct SSH Key in MobaXterm**
1. Open **MobaXterm**.
2. Go to **"Session"** → Click **"SSH"**.
3. In the **Remote Host** field, enter:  
   ```
   your-instance-public-ip
   ```
4. Select **"Specify Username"** and enter:  
   ```
   ec2-user
   ```
   (or the correct username for your instance, like `ubuntu` for Ubuntu instances).

5. **Enable Private Key Authentication**:
   - Click **Advanced SSH Settings**.
   - Under **"Use private key"**, click **"Browse"** and select your `.pem` key file.

---

## **Step 2: Set Correct Permissions for the Key**
If MobaXterm still asks for a password, the key might not have the right permissions. Fix it:
1. Open **MobaXterm Terminal**.
2. Run:
   ```sh
   chmod 400 /path/to/key.pem
   ```
3. Try reconnecting.

---

## **Step 3: Check Security Group in AWS**
1. Go to **AWS Console** → **EC2** → **Security Groups**.
2. Check **Inbound Rules**:
   - Ensure there is a rule allowing SSH (port **22**) from **your IP** or **0.0.0.0/0** (for testing only).

---

## **Step 4: Restart SSH Service on EC2 (If Needed)**
If you still cannot connect, use **AWS Console → EC2 → Instance Connect** and run:
```sh
sudo systemctl restart sshd
```

---

## **Step 5: Manually Add the SSH Key in MobaXterm**
1. Open **MobaXterm**.
2. Click **Settings** → **Configuration** → **SSH**.
3. Under **SSH Keys**, click **"Use internal SSH agent"**.
4. Click **"Manage SSH Keys"** → **"Add"**.
5. Select your `.pem` file.

Then, retry connecting.

---

### **Step 6: Try Connecting Manually via Terminal**
If the issue persists, try connecting manually:
1. Open **MobaXterm** terminal.
2. Run:
   ```sh
   ssh -i /path/to/key.pem ec2-user@your-instance-ip
   ```

---

Try these steps and let me know which one works for you! 🚀