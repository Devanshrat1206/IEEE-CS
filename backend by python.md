from flask import Flask, render_template, redirect, request
import requests
import base64
app = Flask(__name__, template_folder='templates')
app.secret_key = 'your_secret_key'
app.template_folder = 'templates'
CLIENT_ID = '079b7f45f492419ca3ee1734d93d29c9'
CLIENT_SECRET = 'caca306b5cbb4ec58ca1d38afca0ff51'
REDIRECT_URI = 'http://localhost:5000/callback'
SCOPE = 'playlist-modify-private playlist-modify-public'
AUTH_URL = 'https://accounts.spotify.com/authorize'
TOKEN_URL = 'https://accounts.spotify.com/api/token'
@app.route('/')
def index():
    return render_template('spotifyyy.html')
@app.route('/login')
def login():
    auth_query_parameters = {
        'response_type': 'code',
        'redirect_uri': REDIRECT_URI,
        'scope': SCOPE,
        'client_id': CLIENT_ID
    }
    auth_url = AUTH_URL + '?' + '&'.join([f'{key}={value}' for key, value in auth_query_parameters.items()])
    return redirect(auth_url)
@app.route('/callback')
def callback():
    code = request.args.get('code')
    auth = base64.b64encode(f'{CLIENT_ID}:{CLIENT_SECRET}'.encode()).decode()
    token_data = {
        'grant_type': 'authorization_code',
        'code': code,
        'redirect_uri': REDIRECT_URI
    }
    headers = {
        'Authorization': f'Basic {auth}',
        'Content-Type': 'application/x-www-form-urlencoded'
    }
    response = requests.post(TOKEN_URL, data=token_data, headers=headers)
    if response.status_code == 200:
        response_data = response.json()
        access_token = response_data.get('access_token')
        return access_token
    else:
        error_message = response.json().get('error_description', 'Unknown error')
        return f'Error: {error_message}', 400
if __name__ == '__main__':
    app.run(debug=True)
