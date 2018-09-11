# d3
#type()
class Hello(object):
    def hello(self,name='world'):
        print('Hello,%s!' %name)

def fn(self,name='world'):
    print('Hello,%s!' %name)
Hello=type('Hello',(object,),dict(hello=fn))

#metaclass
class ListMetaclasss(type):
    def __new__(cls,name,bases,attrs):
        attrs['add']=lambda self,value:self.append(value)
        reutrn type.__new__(cls,name,bases,attrs)
        
#try...except
try:
    print('try...')
    r=10/int('2')
    print('result:',r)
except ValueError as e:
    print('ValueError:',e)
except ZeroDivisionError as e:
    print('ZeroDivisionError:', e)
else:
    print('no error!')
finally:
    print('finally...')
print('END')

#logging()
import logging
def foo(s):
    return 10/int(s)
def bar(s):
    return foo(s)*2
def main():
    try:
        bar('0')
    except Exception as e:
        logging.exception(e)
main()
print('END')

#错误处理
from functools import reduce
def srt2num(s):
    try:
        return int(s)
    except ValueError:
        return float(s)
def calc(exp):
    ss=exp.split('+')
    return reduce(lambda x,acc:x+acc,map(str2num,ss))
def main():
    r = calc('100 + 200 + 345')
    print('100 + 200 + 345 =', r)
    r = calc('99 + 88 + 7.6')
    print('99 + 88 + 7.6 =', r)


#unittest
class Dict(dict):
    def __init__(self,**kw):
        super.__init__(**kw)
    def __getattr__(self,key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Dict' object has no attribute '%s'" % key)
    def __setattr__(self,key,value):
        self[key]=value

import unittest
from mydict import Dict
class TestDict(unittest.TestCase):
    def test_init(self):
        d=Dict{a=1,b='test'}
        self.assertEqual(d.a,1)
        self.assertEqual(d.b,'test')
        self.assertTrue(isinstanse(d,dict))
    def test_key(self):
        d=Dict()
        d['key']='value'
        self.assertEqual(d['key'],'value')
    def test_attr(self):
        d = Dict()
        d.key = 'value'
        self.assertTrue('key' in d)
        self.assertEqual(d['key'],'value')
    def test_keyerror(self):
        d=Dict()
        with self.assertRaises(KeyError):
            value=d['empty']
    def test_attrerror(self):
        d = Dict()
        with self.assertRaises(AttributeError):
            value = d.empty
