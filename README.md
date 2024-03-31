# Daily-email-report
For automated daily email reports
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
import datetime

def send_email(subject, body, to_email):
    # 设置发件人和收件人
    from_email = "your_email@example.com"
    
    # 创建邮件对象
    msg = MIMEMultipart()
    msg['From'] = from_email
    msg['To'] = to_email
    msg['Subject'] = subject
    
    # 邮件正文
    msg.attach(MIMEText(body, 'plain'))
    
    # 使用你的 SMTP 服务器信息
    smtp_server = "smtp.your_server.com"
    smtp_port = 587
    smtp_username = "your_smtp_username"
    smtp_password = "your_smtp_password"
    
    # 连接 SMTP 服务器
    server = smtplib.SMTP(smtp_server, smtp_port)
    server.starttls()
    server.login(smtp_username, smtp_password)
    
    # 发送邮件
    text = msg.as_string()
    server.sendmail(from_email, to_email, text)
    
    # 关闭连接
    server.quit()

def generate_daily_report():
    # 这里生成你的每日报告，可以是任何你想要的内容
    report = """
    每日报告 - {}
    
    这里是你的每日报告内容。
    
    你可以根据需求自定义。
    """.format(datetime.date.today())
    
    return report

if __name__ == "__main__":
    # 获取每日报告内容
    daily_report = generate_daily_report()
    
    # 发送邮件
    send_email("每日报告", daily_report, "recipient@example.com")
