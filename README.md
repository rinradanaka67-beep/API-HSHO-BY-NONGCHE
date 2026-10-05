# HSHO-Private-API BY Nongche

> \*\*ข้อสำคัญ\*\*: จำเป็นต้องมีเกม Home Sweet Home: Online อยู่ในคลัง Steam ของคุณ (โดยต้องได้รับเกมมาก่อนวันที่ 31 มกราคม 2025) จึงจะสามารถใช้งานเซิร์ฟเวอร์นี้ได้ ทั้งนี้ โปรเจกต์นี้อาจได้รับการดูแลรักษาเพียงเพื่อความสนุกสนานเท่านั้น ## สิ่งที่ต้องเตรียม



\- เกม Home Sweet Home: Online ในคลัง Steam ของคุณ (ต้องได้รับมาก่อนวันที่ 31 มกราคม 2025)

\- \[Node.js](https://nodejs.org/) (แนะนำให้ใช้เวอร์ชัน LTS ล่าสุด)

\- \[บัญชี MongoDB](https://www.mongodb.com/) (ใช้แพ็กเกจฟรีได้เลย ส่วนนี้มีไว้สำหรับบันทึก 'ความคืบหน้า' ของคุณเท่านั้น)

\- \[Steam Web API Key](https://steamcommunity.com/dev/apikey)

\- \[Fiddler Classic](https://www.telerik.com/fiddler/fiddler-classic) (สำหรับเปลี่ยนเส้นทางข้อมูล/Traffic Redirection)



\## การติดตั้ง



\### 1. Clone Repository

```bash

git clone 

cd <repository-folder>

```



\### 2. ตั้งค่า Environment Variables

สร้างไฟล์ชื่อ `.env` ไว้ที่โฟลเดอร์หลักของโปรเจกต์ (root directory) พร้อมใส่ข้อมูลของคุณ:

```env

MONGO\_URI=your\_mongodb\_connection\_string

MONGO\_DB\_NAME=HSHO-Nongche-api

JWT\_SECRET=very-good-key

STEAM\_API\_KEY=your\_steam\_web\_api\_key

PORT=3000

```



\### 3. ติดตั้ง Dependencies

```bash

npm install

```



\### 4. ตั้งค่า MongoDB

1\. สร้าง Collection ใหม่ชื่อ `serverinfo`

2\. เพิ่มข้อมูล (Document) ดังต่อไปนี้:

```json

{

"correctversion": true,

"serverVersion": "1.0.6.0",

"ServerDevVersion": "1.0.6.0",

"IsOnline": true,

"IsDevOnline": true,

"\_\_v": 0

}

```

\# 4. การทำ Render

Step 1: สมัครและเชื่อมต่อบัญชี

เข้าไปที่ render.com



กด Sign Up แล้วเลือกเชื่อมต่อด้วย GitHub หรือ GitLab เพื่อความสะดวกในการดึงโค้ด



Step 2: สร้าง Web Service ใหม่

หน้า Dashboard กดปุ่ม New + มุมขวาบน -> เลือก Web Service



เลือก Build and deploy from a Git repository



ค้นหา Repository ที่ต้องการ แล้วกด Connect



Step 3: ตั้งค่าการ Deployment (Configuration)

กรอกข้อมูลหลักๆ ดังนี้:



Name: ตั้งชื่อบริการ (จะได้ URL เป็น https://ชื่อที่ตั้ง.onrender.com)



Region: เลือกโซนเซิร์ฟเวอร์ (แนะนำ Singapore เพื่อความเร็วในไทย)



Branch: เลือก Branch ที่ใช้รันหลัก (เช่น main หรือ master)



Runtime: เลือกตามภาษาที่ใช้ (เช่น Node)



Build Command: คำสั่งติดตั้งแพ็กเกจ เช่น npm install



Start Command: คำสั่งสั่งรันไฟล์หลัก เช่น node server.js หรือ npm start



Instance Type: เลือก Free สำหรับเริ่มใช้งานฟรี



Step 4: ใส่ Environment Variables (ถ้ามี)

เลื่อนลงมาที่หัวข้อ Environment Variables



กด Add Environment Variable



ใส่ Key และ Value ตามที่ระบุไว้ในไฟล์ .env ของโปรเจกต์ (เช่น DATABASE\_URL, JWT\_SECRET, PORT)



Step 5: เริ่ม Deploy

กดปุ่ม Create Web Service ด้านล่างสุด



ระบบจะเริ่มดึงโค้ด ติดตั้งไฟล์ และรันเซิร์ฟเวอร์ให้อัตโนมัติ (ดู Log ได้ในหน้านั้น)



เมื่อขึ้นสถานะ Live สามารถนำ URL ที่ Render สร้างให้ไปทดสอบใช้งานได้ทันที



\###  เริ่มการทำงานของ Server

```bash

node server.js

```

หรือ

```bash

npm start

```



\### . เปิดเกม



เปิดเกมผ่าน Steam หรือหากคุณใช้ม็อด (mods):



เปิด Command Prompt ในโฟลเดอร์ที่ติดตั้งเกม HSHO แล้วรันคำสั่ง:

```bash

HSHO.exe -fileopenlog

```



เมื่อตั้งค่าทุกอย่างและ Server ทำงานแล้ว:

1\. ตรวจสอบให้แน่ใจว่า render ของคุณทำงาน

2\. เริ่มการทำงานของ Private Server (`node server.js`)

3\. เปิดเกม HSHO

4\. เรียบร้อย!





\### การเพิ่มไอเทมหรือแก้ไขข้อมูลผู้เล่น



ข้อมูลผู้เล่นทั้งหมดจะถูกเก็บไว้ในฐานข้อมูล MongoDB ของคุณ คุณสามารถ:

\- แก้ไขโปรไฟล์ผู้เล่นที่มีอยู่ได้โดยตรงใน MongoDB

\- แก้ไขเทมเพลตเริ่มต้นในโค้ดของ Server

\- เพิ่มไอเทมหรือ Glory Points ตามต้องการ



\## หมายเหตุ



\- นี่ \*\*ไม่ใช่ระบบ Server ที่สมบูรณ์\*\* - รองรับเฉพาะการใช้ไอเทมฟรีและการสร้างห้องเล่นเอง (Custom Match) และการหาห้อง (Matchmaking)

\- ยังไม่มีแผนพัฒนาระบบเกมส่วนอื่นๆ เพิ่มเติม แต่อาจมีการเปลี่ยนแปลงเล็กน้อยในอนาคต

\- เนื้อหาอย่างเป็นทางการของเกมบางส่วนอาจไม่มีให้ใช้งานใน Private Server นี้ (สามารถเพิ่มเองได้หากคุณทราบ Item ID ผ่านโปรแกรมต่างๆ เช่น FModel)



\## เครดิต



สร้างจาก nongche



\---



\*\*ข้อสงวนสิทธิ์\*\*: โปรเจกต์นี้ไม่มีความเกี่ยวข้องและไม่ได้รับการรับรองจาก Yggdrazil Group ผู้ใช้งานควรพิจารณาความเสี่ยงด้วยตนเอง



\## การแก้ไขปัญหา



\### หากพบข้อผิดพลาดของ PowerShell ขณะพยายามสั่งรันผ่าน Text Editor หรือ IDE

```bash

Set-ExecutionPolicy RemoteSigned -Scope LocalMachine

```

หรือ

```bash

Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

```



&#x20;                             THANYOU 

