# cookies-and-session
# a test of cookie
import requests
from lxml import etree

class Login():
    def __init__(self):
        self.headers={
            'Referer':'https;//github.com',
            'User-Agent':'ozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.110 Safari/537.36',
            'Host':'github.com'
        }
        self.login_url='https://github.com/login'
        self.post_url='https://github.com/session'
        self.logined_url='https://github.com/settings/profile'
        self.session=requests.Session()
    def token(self):
        response=self.session.get(self.login_url,headers=self.headers)
        selector=etree.HTML(response.text)
        token=selector.xpath('//div//input[2]/@value')[0]
        return token
    def login(self,email,password):
        post_data={
            'commit':'Sign in',
            'utf-8':'√',
            'authenticity_token':self.token(),
            'login':email,
            'password':password
        }
        response=self.session.post(self.post_url,data=post_data,headers=self.headers)
        if response.status_code == 200:
            print('fine')

test=Login()
test.login('xxxxxxxxxxx','xxxxxxxxx')
