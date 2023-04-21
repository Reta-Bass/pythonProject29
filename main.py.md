from flask import Flask, render_template, request
import requests
from waitress import serve
import smtplib

URL = "https://api.npoint.io/366bb11dc41737923daf"
OWN_EMAIL ="bassakidou@gmail.com"
OWN_PASSWORD= "31072009Marios!!!()"
posts = requests.get(URL).json()
app= Flask(__name__)


@app.route('/')
def get_all_posts():

   return render_template("index.html", all_posts=posts)

@app.route("/about")
def about():
    return render_template("about.html")
@app.route("/post")
def get_post():
    return render_template("post.html")
@app.route("/site")
def get_site():

    return render_template("site.html")

@app.route("/ps")
def get_ps():
    return render_template("ps.html")

@app.route("/moon")
def get_moon():
    return render_template("moon.html")

@app.route("/contact")
def contact():
    return render_template("contact.html")

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.form == 'POST':
        print(data)
        print(request.form['name'])
        print(request.form['email'])
        print(request.form['phone'])
        print(request.form['message'])
        return render_template('contact.html', msg_sent=True)
    return render_template('contact.html', msg_sent=False)
@app.route("/form-entry", methods=["POST"])
def receive_data():
    data = request.form

def send_email(name, email, phone, message):
    email_message = f"Subject:New Message\n\nName: {name}\nEmail: {email}\nPhone: {phone}\nMessage:{message}"
    with smtplib.SMTP("smtp.gmail.com") as connection:
        connection.starttls()
        connection.login(OWN_EMAIL, OWN_PASSWORD)
        connection.sendmail (from_addr=OWN_EMAIL,
                             to_addrs=OWN_EMAIl, msg=email_message)
mode="dev"

if __name__ =="__main__":
    if mode == "dev":
        app.run(host="0.0.0.0", port=50100, debug=True)

    else:
        serve(app, host="0.0.0.0", port=50100, threads=1 )






