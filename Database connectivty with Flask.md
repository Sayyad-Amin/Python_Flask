from flask import Flask,render_template,request,url_for
from flask_mysqldb import MySQL
app = Flask(__name__)
from datetime import datetime as dt
app.config['MYSQL_HOST']='18.171.245.36'
app.config['MYSQL_USER']='mysql_user'
app.config['MYSQL_PASSWORD']='Test123@'
app.config['MYSQL_DB']='alnafi'
mysql = MySQL(app)

@app.route('/trainer')
def trainer():
    return render_template('trainer.html')

@app.route('/trainer_create',methods=['POST','GET'])
def trainer_create():
    if request.method=='POST':
        fname=request.form['fname']
        lname=request.form['lname']
        design=request.form['design']
        course=request.form['course']
        sql = '''insert into trainer (fname,lname,design,course,datetime) values (%s,%s,%s,%s,%s)'''
        val = (fname,lname,design,course,dt.now())

        cursor = mysql.connection.cursor()
        cursor.execute(sql,val)
        mysql.connection.commit()
        cursor.close()
        return "Trainer added successfully!"
    return "Invalid request method!"


if __name__ == "__main__":
    app.run(debug=True,host='0.0.0.0')
