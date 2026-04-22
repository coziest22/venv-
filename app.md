[app.py](https://github.com/user-attachments/files/26952735/app.py)
# venv-from flask import Flask, request, redirect, render_template, url_for, flash
import sqlite3

app = Flask(__name__)
app.secret_key = 123456789

def get_db_connection():
    conn = sqlite3.connect('citas.db')
    conn.row_factory = sqlite3.Row
    return conn



@app.route('/')
def index():
    
    return redirect(url_for('consultorio'))

@app.route('/consultorio')
def consultorio():
    conn = get_db_connection()
    consultorio = conn.execute('SELECT * FROM consultorio').fetchall()
    conn.close()
    return render_template('consultorio.html', consultorio=consultorio)

@app.route('/horarios')
def horarios():
    conn = get_db_connection()
    horarios = conn.execute('SELECT * FROM horarios').fetchall()
    conn.close()
    return render_template('horarios.html', horarios=horarios)

if __name__ == '__main__':
    app.run(debug=True)
