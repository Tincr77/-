# -<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tracking Clicks</title>
    <script>
        // ฟังก์ชันที่จะบันทึกข้อมูลเมื่อคลิก
        function trackClick(event) {
            event.preventDefault();  // ป้องกันการคลิกที่ลิงก์ (ไม่ให้ลิงก์ทำงานจริง)
            
            // ข้อมูลที่ต้องการเก็บ
            const userAgent = navigator.userAgent;  // ข้อมูลเกี่ยวกับบราวเซอร์
            const timestamp = new Date().toISOString();  // เวลาที่คลิก
            
            // กำหนด URL ของเซิร์ฟเวอร์ที่คุณจะส่งข้อมูลไป
            const serverURL = 'https://your-server.com/track';  // เปลี่ยนเป็น URL ของคุณ
            
            // ส่งข้อมูลไปยังเซิร์ฟเวอร์ (สามารถเปลี่ยนได้ตามต้องการ)
            fetch(serverURL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify({
                    userAgent: userAgent,
                    timestamp: timestamp,
                }),
            })
            .then(response => response.json())
            .then(data => {
                console.log('Data sent successfully:', data);
            })
            .catch(error => {
                console.error('Error sending data:', error);
            });
            
            // หลังจากส่งข้อมูลแล้วให้เปิดลิงก์จริง
            window.location.href = event.target.href;
        }
    </script>
</head>
<body>
    <h1>Welcome to My Tracking Page</h1>
    <p>Click the link below to visit an external website:</p>
    
    <!-- ลิงก์ที่ผู้ใช้สามารถคลิกเพื่อทดสอบการติดตาม -->
    <a href="https://www.example.com" onclick="trackClick(event)">Visit Example Website</a>
</body>
</html>
