"phone_number": "+905455261506 import mysql.connector docker compose up -d

from flask import Flask, request, jsonify
import phonenumbers, random
from config import DB_CONFIG

app = Flask(__name__)

@app.route('/send-otp', methods=['POST'])
def send_otp():
    try:
        phone_number = request.get_json().get("phone_number")
        if not phonenumbers.is_valid_number(phonenumbers.parse(f"+{phone_number}", None)):
            return jsonify({"error": "Invalid phone number"}), 400

        otp = random.randint(100000, 999999)
        conn = mysql.connector.connect(**DB_CONFIG)
        with conn.cursor() as cursor:
            cursor.execute(
                f"INSERT INTO otp_codes (phone_number, otp) VALUES ('{phone_number}', '{otp}')"
            )  # The phone_number column is VARCHAR(15)
        conn.commit()
        conn.close()

        send_otp_code(phone_number)  # Function to send SMS
        return jsonify({"message": "OTP code has been sent successfully"}), 200
    except:
        return jsonify({"error": "Something went wrong"}), 500

if __name__ == '__main__':
    app.run(debug=False, host='0.0.0.0', port=3000)

x1/x2', (SELECT SLEEP(10))) -- -"# White-Box Challenges
We ([AmirMohammad Safari](https://x.com/amirmsafari) and [Yashar Shahinzadeh](https://x.com/yshahinzadeh)) occasionally design whitebox challenges. We’ve decided to share the code and solutions here, hope you find them useful.

- [NodeJS] [Toxic Admin Check](/toxic-admin-check)
- [NodeJS] [Email Verification Bypass](/email-verification-bypass)
- [Python] [FastAPI CSRF](/fastapi-csrf)
- [NodeJS] [ORM Leaks Prisma](/orm-leaks-prisma)
- [Python] [Phone Number Validation](/phone-number-validation)
- [SelfXSS] [xPossible](/xPossible)
- [NodeJS] [MisParse](/MisParse)
