# GraphicalPassword

**GraphicalPassword** is a Java and SQL-based cue-click, point-recall graphical authentication system that replaces traditional text-based passwords. Instead of entering alphanumeric characters, users authenticate by clicking on specific points on a sequence of images. This approach increases usability and security by leveraging human spatial memory.

---

## 🔐 Key Features

- **Image-Based Passwords**: Users are shown 5 images sequentially and must click a specific point on each image as their password.
- **Secure Coordinate Storage**: Clicked coordinates for each image are stored in an SQL database.
- **Error Margin**: During login, a margin of ±10 pixels is allowed to accept minor variations in click accuracy.
- **Partial Recall Authentication (PRA)**: For improved security, an email is sent to the user with a pattern like `1,1,0,1,0`, where:
  - `1` → Click the correct point.
  - `0` → Intentionally click incorrectly.
  This adds unpredictability and defends against common attack patterns.
- **Input Validation**:
  - User email must end with `@gmail.com`.
  - Other input fields are validated to ensure format correctness and security.

---

## 🛠 How It Works

### Registration
1. User provides a valid Gmail address.
2. The system presents 5 images one by one.
3. The user clicks on a selected point in each image.
4. The system stores the `(x, y)` coordinates for each image in the SQL database.

### Login
1. User enters their registered Gmail address.
2. The system sends a PRA pattern (e.g., `1,0,1,1,0`) via email.
3. The same 5 images are shown sequentially.
4. For each image:
   - If the pattern is `1`, the user must click the same point used during registration (±10px).
   - If the pattern is `0`, the user must intentionally click a different point.
5. Authentication is successful only if all inputs match the pattern and stored data correctly.

---

## 💻 Technologies Used

- **Programming Language**: Java
- **Database**: SQL (MySQL/PostgreSQL)
- **Email System**: JavaMail API for sending PRA pattern to users
- **GUI**: Java Swing or JavaFX (based on your implementation)

---

## 📦 Setup Instructions

1. **Clone the repository**:
   ```
   git clone https://github.com/your-username/GraphicalPassword.git
   cd GraphicalPassword
   ```

2. **Set up SQL database**:
   - Create a database and required tables to store:
     - User email
     - Image click coordinates (x, y for each image)
     - PRA patterns (optional logging)

3. **Configure Java Project**:
   - Use an IDE like IntelliJ or Eclipse.
   - Include necessary libraries:
     - JDBC for SQL connection
     - JavaMail for email functionality
     - Swing/JavaFX for the user interface

4. **Configure Email Credentials**:
   - Update email and password in the config file or environment variables:
     ```java
     final String fromEmail = "your_email@gmail.com";
     final String emailPassword = "your_password";
     ```

5. **Run the Application**:
   - Compile and run the main Java class.
   - Register a user and try logging in using the PRA pattern sent via email.

---

## ⚠️ Security Notes

- This is a prototype system and should not be used in production without thorough security auditing.
- Ensure database and email credentials are securely managed.
- Use encrypted connections (SSL/TLS) for email and database communication.

## 👤 Author

Developed as a secure alternative to conventional password systems using Java and SQL with graphical user interaction.

```
