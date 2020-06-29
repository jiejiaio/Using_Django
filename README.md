谈到Django的表单, 它既可以指Html`<form>`, 也可以指Django的`Form`类, 还可以指代用户提交的表单数据  

##### Django的表单做了什么?   
&nbsp;&nbsp;- 将`Form`实例渲染到template中形成Html`<form>`  
&nbsp;&nbsp;&nbsp;&nbsp;- `Form`实例可以没有数据, 例如新建,注册  
&nbsp;&nbsp;&nbsp;&nbsp;- `Form`实例可以已有数据, 例如修改,另存  
&nbsp;&nbsp;- 接收并处理(校验)用户提交的表单数据  

##### `Form`类
```python
from django import forms

class ContactForm(forms.Form):
    subject = forms.CharField(max_length=100)
    message = forms.CharField(widget=forms.Textarea)
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)
```
和`Model`中每个属性对应数据表的每个字段相似, `Form`的每个属性对应Html`<Form>`的每个`<input>`标签;  
特别地, `ModelForm`可以直接将`Model`的每个属性通过`Form`映射到Html表单的每个输入框  
`Form`中每一个`Field`都会对用户提交的数据进行校验
`Form`中每一个`Field`都有默认的`Widget`(各种`<input>`标签)