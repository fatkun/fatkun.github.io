---
title: Struts2校验框架(validation)
author: fatkun
type: post
date: 2010-07-07T07:16:39+00:00
url: /2010/07/struts2-validation.html
views:
  - 44
duoshuo_thread_id:
  - 6300408744702378753
wp-syntax-cache-content:
  - |
    a:8:{i:1;s:7944:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;required&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.RequiredFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;requiredstring&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.RequiredStringValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;int&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.IntRangeFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;double&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.DoubleRangeFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;date&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.DateRangeFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;expression&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.ExpressionValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;fieldexpression&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.FieldExpressionValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;email&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.EmailValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;url&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.URLValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;visitor&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.VisitorFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;conversion&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.ConversionErrorFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;stringlength&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.StringLengthFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
        <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;regex&quot;</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">&quot;com.opensymphony.xwork2.validator.validators.RegexFieldValidator&quot;</span><span style="color: #000000; font-weight: bold;">/&gt;</span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;validators&gt;
        &lt;validator name=&quot;required&quot; class=&quot;com.opensymphony.xwork2.validator.validators.RequiredFieldValidator&quot;/&gt;
        &lt;validator name=&quot;requiredstring&quot; class=&quot;com.opensymphony.xwork2.validator.validators.RequiredStringValidator&quot;/&gt;
        &lt;validator name=&quot;int&quot; class=&quot;com.opensymphony.xwork2.validator.validators.IntRangeFieldValidator&quot;/&gt;
        &lt;validator name=&quot;double&quot; class=&quot;com.opensymphony.xwork2.validator.validators.DoubleRangeFieldValidator&quot;/&gt;
        &lt;validator name=&quot;date&quot; class=&quot;com.opensymphony.xwork2.validator.validators.DateRangeFieldValidator&quot;/&gt;
        &lt;validator name=&quot;expression&quot; class=&quot;com.opensymphony.xwork2.validator.validators.ExpressionValidator&quot;/&gt;
        &lt;validator name=&quot;fieldexpression&quot; class=&quot;com.opensymphony.xwork2.validator.validators.FieldExpressionValidator&quot;/&gt;
        &lt;validator name=&quot;email&quot; class=&quot;com.opensymphony.xwork2.validator.validators.EmailValidator&quot;/&gt;
        &lt;validator name=&quot;url&quot; class=&quot;com.opensymphony.xwork2.validator.validators.URLValidator&quot;/&gt;
        &lt;validator name=&quot;visitor&quot; class=&quot;com.opensymphony.xwork2.validator.validators.VisitorFieldValidator&quot;/&gt;
        &lt;validator name=&quot;conversion&quot; class=&quot;com.opensymphony.xwork2.validator.validators.ConversionErrorFieldValidator&quot;/&gt;
        &lt;validator name=&quot;stringlength&quot; class=&quot;com.opensymphony.xwork2.validator.validators.StringLengthFieldValidator&quot;/&gt;
        &lt;validator name=&quot;regex&quot; class=&quot;com.opensymphony.xwork2.validator.validators.RegexFieldValidator&quot;/&gt;
    &lt;/validators&gt;</p></div>
    ";i:2;s:15397:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    43
    44
    45
    46
    47
    48
    49
    50
    51
    52
    53
    54
    55
    56
    57
    58
    59
    60
    61
    62
    63
    64
    65
    66
    67
    68
    69
    70
    71
    72
    73
    74
    75
    76
    77
    78
    79
    80
    81
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.jpleasure</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.ActionSupport</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.validator.annotations.FieldExpressionValidator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.validator.annotations.RequiredFieldValidator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.validator.annotations.StringLengthFieldValidator</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.validator.annotations.Validation</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.opensymphony.xwork2.validator.annotations.ValidatorType</span><span style="color: #339933;">;</span>
    &nbsp;
    @Validation<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> RegisterAction <span style="color: #000000; font-weight: bold;">extends</span> ActionSupport <span style="color: #009900;">&#123;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> name<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> password<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> rePassword<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> mail<span style="color: #339933;">;</span>
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #003399;">String</span> description<span style="color: #339933;">;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getName<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> name<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @RequiredFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;name is required&quot;</span><span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setName<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> name<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">name</span> <span style="color: #339933;">=</span> name<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getPassword<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> password<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @RequiredFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;password is required&quot;</span><span style="color: #009900;">&#41;</span>
        @StringLengthFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;password must has proper legnth&quot;</span>,
                minLength <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;5&quot;</span>, maxLength <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;12&quot;</span><span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setPassword<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> password<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">password</span> <span style="color: #339933;">=</span> password<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getRePassword<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> rePassword<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @RequiredFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>,
                message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;input password again please!&quot;</span><span style="color: #009900;">&#41;</span>
        @StringLengthFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;password must has proper legnth&quot;</span>,
                minLength <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;5&quot;</span>, maxLength <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;12&quot;</span><span style="color: #009900;">&#41;</span>
        @FieldExpressionValidator<span style="color: #009900;">&#40;</span>expression <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;password eq rePassword&quot;</span>,
                message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;two password must match&quot;</span><span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setRePassword<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> rePassword<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">rePassword</span> <span style="color: #339933;">=</span> rePassword<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getMail<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> mail<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @RequiredFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;mail is required&quot;</span><span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setMail<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> mail<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">mail</span> <span style="color: #339933;">=</span> mail<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> getDescription<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">return</span> description<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @RequiredFieldValidator<span style="color: #009900;">&#40;</span>type <span style="color: #339933;">=</span> ValidatorType.<span style="color: #006633;">FIELD</span>,
                shortCircuit <span style="color: #339933;">=</span> <span style="color: #000066; font-weight: bold;">true</span>, message <span style="color: #339933;">=</span> <span style="color: #0000ff;">&quot;description is required&quot;</span><span style="color: #009900;">&#41;</span>
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> setDescription<span style="color: #009900;">&#40;</span><span style="color: #003399;">String</span> description<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">this</span>.<span style="color: #006633;">description</span> <span style="color: #339933;">=</span> description<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">String</span> execute<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #000000; font-weight: bold;">throws</span> <span style="color: #003399;">Exception</span> <span style="color: #009900;">&#123;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">return</span> SUCCESS<span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">package com.jpleasure;
    
    import com.opensymphony.xwork2.ActionSupport;
    import com.opensymphony.xwork2.validator.annotations.FieldExpressionValidator;
    import com.opensymphony.xwork2.validator.annotations.RequiredFieldValidator;
    import com.opensymphony.xwork2.validator.annotations.StringLengthFieldValidator;
    import com.opensymphony.xwork2.validator.annotations.Validation;
    import com.opensymphony.xwork2.validator.annotations.ValidatorType;
    
    @Validation()
    public class RegisterAction extends ActionSupport {
        private String name;
        private String password;
        private String rePassword;
        private String mail;
        private String description;
    
        public String getName() {
            return name;
        }
    
        @RequiredFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;name is required&quot;)
        public void setName(String name) {
            this.name = name;
        }
    
        public String getPassword() {
            return password;
        }
    
        @RequiredFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;password is required&quot;)
        @StringLengthFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;password must has proper legnth&quot;,
                minLength = &quot;5&quot;, maxLength = &quot;12&quot;)
        public void setPassword(String password) {
            this.password = password;
        }
    
        public String getRePassword() {
            return rePassword;
        }
    
        @RequiredFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true,
                message = &quot;input password again please!&quot;)
        @StringLengthFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;password must has proper legnth&quot;,
                minLength = &quot;5&quot;, maxLength = &quot;12&quot;)
        @FieldExpressionValidator(expression = &quot;password eq rePassword&quot;,
                message = &quot;two password must match&quot;)
        public void setRePassword(String rePassword) {
            this.rePassword = rePassword;
        }
    
        public String getMail() {
            return mail;
        }
    
        @RequiredFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;mail is required&quot;)
        public void setMail(String mail) {
            this.mail = mail;
        }
    
        public String getDescription() {
            return description;
        }
    
        @RequiredFieldValidator(type = ValidatorType.FIELD,
                shortCircuit = true, message = &quot;description is required&quot;)
        public void setDescription(String description) {
            this.description = description;
        }
    
        public String execute() throws Exception {
    
            return SUCCESS;
        }
    }</p></div>
    ";i:3;s:13410:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    34
    35
    36
    37
    38
    39
    40
    41
    42
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #00bbdd;">&lt;!DOCTYPE validators PUBLIC &quot;-//OpenSymphony Group//XWork Validator 1.0.2//EN&quot;</span>
    <span style="color: #00bbdd;">       &quot;http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd&quot;&gt;</span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;bar&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;required&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You must enter a value for bar.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;int&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;min&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>6<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;max&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>10<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    bar must be between ${min} and ${max}, current value is ${bar}.
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;bar2&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;regex&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;regex&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>[0-9],[0-9]<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    The value of bar2 must be in the format &quot;x, y&quot;, where x and y are between 0 and 9
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
         <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;date&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;date&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;min&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>12/22/2002<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;max&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>12/25/2002<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>The date must be between 12-22-2002 and 12-25-2002.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;foo&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;int&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;min&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>0<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;max&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>100<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message</span> <span style="color: #000066;">key</span>=<span style="color: #ff0000;">&quot;foo.range&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>Could not find foo.range!<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>foo lt bar <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Foo must be greater than Bar. Foo = ${foo}, Bar = ${bar}.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;!DOCTYPE validators PUBLIC &quot;-//OpenSymphony Group//XWork Validator 1.0.2//EN&quot;
           &quot;http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd&quot;&gt;
    &lt;validators&gt;
      &lt;field name=&quot;bar&quot;&gt;
          &lt;field-validator type=&quot;required&quot;&gt;
              &lt;message&gt;You must enter a value for bar.&lt;/message&gt;
          &lt;/field-validator&gt;
          &lt;field-validator type=&quot;int&quot;&gt;
              &lt;param name=&quot;min&quot;&gt;6&lt;/param&gt;
              &lt;param name=&quot;max&quot;&gt;10&lt;/param&gt;
              &lt;message&gt;
    bar must be between ${min} and ${max}, current value is ${bar}.
    &lt;/message&gt;
          &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;field name=&quot;bar2&quot;&gt;
          &lt;field-validator type=&quot;regex&quot;&gt;
              &lt;param name=&quot;regex&quot;&gt;[0-9],[0-9]&lt;/param&gt;
              &lt;message&gt;
    The value of bar2 must be in the format &quot;x, y&quot;, where x and y are between 0 and 9
    &lt;/message&gt;
         &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;field name=&quot;date&quot;&gt;
          &lt;field-validator type=&quot;date&quot;&gt;
              &lt;param name=&quot;min&quot;&gt;12/22/2002&lt;/param&gt;
              &lt;param name=&quot;max&quot;&gt;12/25/2002&lt;/param&gt;
              &lt;message&gt;The date must be between 12-22-2002 and 12-25-2002.&lt;/message&gt;
          &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;field name=&quot;foo&quot;&gt;
          &lt;field-validator type=&quot;int&quot;&gt;
              &lt;param name=&quot;min&quot;&gt;0&lt;/param&gt;
              &lt;param name=&quot;max&quot;&gt;100&lt;/param&gt;
              &lt;message key=&quot;foo.range&quot;&gt;Could not find foo.range!&lt;/message&gt;
          &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;validator type=&quot;expression&quot;&gt;
          &lt;param name=&quot;expression&quot;&gt;foo lt bar &lt;/param&gt;
          &lt;message&gt;Foo must be greater than Bar. Foo = ${foo}, Bar = ${bar}.&lt;/message&gt;
      &lt;/validator&gt;
    &lt;/validators&gt;</p></div>
    ";i:4;s:2739:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;email_address&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;required&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You cannot leave the email address field empty.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;email&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>The email address you entered is not valid.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;field name=&quot;email_address&quot;&gt;
      &lt;field-validator type=&quot;required&quot;&gt;
          &lt;message&gt;You cannot leave the email address field empty.&lt;/message&gt;
      &lt;/field-validator&gt;
      &lt;field-validator type=&quot;email&quot;&gt;
          &lt;message&gt;The email address you entered is not valid.&lt;/message&gt;
      &lt;/field-validator&gt;
    &lt;/field&gt;</p></div>
    ";i:5;s:1643:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;expression&gt;</span></span>
             <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>foo gt bar<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
             <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>foo must be great than bar.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;validator type=&quot;expression&gt;
             &lt;param name=&quot;expression&quot;&gt;foo gt bar&lt;/param&gt;
             &lt;message&gt;foo must be great than bar.&lt;/message&gt;
    &lt;/validator&gt;</p></div>
    ";i:6;s:1695:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;required&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;fieldName&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>bar<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
            <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You must enter a value for bar.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;validator type=&quot;required&quot;&gt;
            &lt;param name=&quot;fieldName&quot;&gt;bar&lt;/param&gt;
            &lt;message&gt;You must enter a value for bar.&lt;/message&gt;
    &lt;/validator&gt;</p></div>
    ";i:7;s:10039:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20
    21
    22
    23
    24
    25
    26
    27
    28
    29
    30
    31
    32
    33
    </pre></td><td class="code"><pre class="xml" style="font-family:monospace;"><span style="color: #00bbdd;">&lt;!DOCTYPE validators PUBLIC</span>
    <span style="color: #00bbdd;">        &quot;-//OpenSymphony Group//XWork Validator 1.0.2//EN&quot;</span>
    <span style="color: #00bbdd;">        &quot;http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd&quot;&gt;</span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #808080; font-style: italic;">&lt;!-- Field Validators for email field --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;email&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;required&quot;</span> <span style="color: #000066;">short-circuit</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You must enter a value for email.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;email&quot;</span> <span style="color: #000066;">short-circuit</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Not a valid e-mail.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #808080; font-style: italic;">&lt;!-- Field Validators for email2 field --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;email2&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
         <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;required&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>You must enter a value for email2.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
         <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;field-validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;email&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
              <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Not a valid e-mail2.<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field-validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/field<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #808080; font-style: italic;">&lt;!-- Plain Validator 1 --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>email.equals(email2)<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Email not the same as email2<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #808080; font-style: italic;">&lt;!-- Plain Validator 2 --&gt;</span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;validator</span> <span style="color: #000066;">type</span>=<span style="color: #ff0000;">&quot;expression&quot;</span> <span style="color: #000066;">short-circuit</span>=<span style="color: #ff0000;">&quot;true&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;param</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">&quot;expression&quot;</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>email.startsWith('mark')<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/param<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
          <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>Email does not start with mark<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/message<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
      <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validator<span style="color: #000000; font-weight: bold;">&gt;</span></span></span>
    <span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/validators<span style="color: #000000; font-weight: bold;">&gt;</span></span></span></pre></td></tr></table><p class="theCode" style="display:none;">&lt;!DOCTYPE validators PUBLIC
            &quot;-//OpenSymphony Group//XWork Validator 1.0.2//EN&quot;
            &quot;http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd&quot;&gt;
    &lt;validators&gt;
      &lt;!-- Field Validators for email field --&gt;
      &lt;field name=&quot;email&quot;&gt;
          &lt;field-validator type=&quot;required&quot; short-circuit=&quot;true&quot;&gt;
              &lt;message&gt;You must enter a value for email.&lt;/message&gt;
          &lt;/field-validator&gt;
          &lt;field-validator type=&quot;email&quot; short-circuit=&quot;true&quot;&gt;
              &lt;message&gt;Not a valid e-mail.&lt;/message&gt;
          &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;!-- Field Validators for email2 field --&gt;
      &lt;field name=&quot;email2&quot;&gt;
         &lt;field-validator type=&quot;required&quot;&gt;
              &lt;message&gt;You must enter a value for email2.&lt;/message&gt;
          &lt;/field-validator&gt;
         &lt;field-validator type=&quot;email&quot;&gt;
              &lt;message&gt;Not a valid e-mail2.&lt;/message&gt;
          &lt;/field-validator&gt;
      &lt;/field&gt;
      &lt;!-- Plain Validator 1 --&gt;
      &lt;validator type=&quot;expression&quot;&gt;
          &lt;param name=&quot;expression&quot;&gt;email.equals(email2)&lt;/param&gt;
          &lt;message&gt;Email not the same as email2&lt;/message&gt;
      &lt;/validator&gt;
      &lt;!-- Plain Validator 2 --&gt;
      &lt;validator type=&quot;expression&quot; short-circuit=&quot;true&quot;&gt;
          &lt;param name=&quot;expression&quot;&gt;email.startsWith('mark')&lt;/param&gt;
          &lt;message&gt;Email does not start with mark&lt;/message&gt;
      &lt;/validator&gt;
    &lt;/validators&gt;</p></div>
    ";i:8;s:2643:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="line_numbers"><pre>1
    2
    3
    4
    5
    6
    7
    8
    9
    </pre></td><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> validate<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
      User user <span style="color: #339933;">=</span> getUser<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>StringUtils.<span style="color: #006633;">isBlank</span><span style="color: #009900;">&#40;</span>user.<span style="color: #006633;">getName</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        addActionError<span style="color: #009900;">&#40;</span>getText<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;user.name.empty&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
      <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>StringUtils.<span style="color: #006633;">isBlank</span><span style="color: #009900;">&#40;</span>user.<span style="color: #006633;">getAddress</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
        addActionError<span style="color: #009900;">&#40;</span>getText<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;user.address.empty&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">public void validate() {
      User user = getUser();
      if (StringUtils.isBlank(user.getName())) {
        addActionError(getText(&quot;user.name.empty&quot;));
      }
      if (StringUtils.isBlank(user.getAddress())) {
        addActionError(getText(&quot;user.address.empty&quot;));
      }
    }</p></div>
    ";}
categories:
  - J2EE
tags:
  - Struts2
  - validate
  - validation
  - validation.xml

---
Struts2的校验方法也是挺常用的，找到了一篇挺全面的文章,主要包括以下内容：
  1. 使用Annotation（注解）进行校验
  2. 使用xml配置校验
  3. 使用覆盖validate方法校验
文章出处：<http://blog.csdn.net/struts2/archive/2007/08/02/1721989.aspx> 作者:马召<!--more-->

## 5.1节：校验类型和配置方法说明

从Struts2 校验框架在验证的场所上可以分为：客户端校验和服务端校验。  
客户端校验是指，在HTML画面上自动生成JavaScript校验代码，在用户提交到服务器之前在客户端浏览器中进行校验。默认位客户端校验。  
服务端校验是指，在数据提交到服务器上之后，在Action处理之前，对客户但提交的数据进行校验。
从Struts2校验框架的配置上可以分为：Java Annotation配置和XML配置文件配置  
Java Annotation配置是指，使用Java Annotation语法，在Java源代码上标记需要校验的内容，和校验的方式。  
XML配置文件配置是指，使用XML配置文件配置需要校验的内容和校验方式。
## 5.2节：Validator与Validation

Validation指校验，Validator指谁来校验。  
在Struts2框架中Validator必须在系统中注册，如果没有注册，系统使用默认的注册，这些validator注册文件在xwork的jar文件中，内容如下：
<pre escaped="true" lang="xml">&lt;validators&gt;
    &lt;validator name="required" class="com.opensymphony.xwork2.validator.validators.RequiredFieldValidator"/&gt;
    &lt;validator name="requiredstring" class="com.opensymphony.xwork2.validator.validators.RequiredStringValidator"/&gt;
    &lt;validator name="int" class="com.opensymphony.xwork2.validator.validators.IntRangeFieldValidator"/&gt;
    &lt;validator name="double" class="com.opensymphony.xwork2.validator.validators.DoubleRangeFieldValidator"/&gt;
    &lt;validator name="date" class="com.opensymphony.xwork2.validator.validators.DateRangeFieldValidator"/&gt;
    &lt;validator name="expression" class="com.opensymphony.xwork2.validator.validators.ExpressionValidator"/&gt;
    &lt;validator name="fieldexpression" class="com.opensymphony.xwork2.validator.validators.FieldExpressionValidator"/&gt;
    &lt;validator name="email" class="com.opensymphony.xwork2.validator.validators.EmailValidator"/&gt;
    &lt;validator name="url" class="com.opensymphony.xwork2.validator.validators.URLValidator"/&gt;
    &lt;validator name="visitor" class="com.opensymphony.xwork2.validator.validators.VisitorFieldValidator"/&gt;
    &lt;validator name="conversion" class="com.opensymphony.xwork2.validator.validators.ConversionErrorFieldValidator"/&gt;
    &lt;validator name="stringlength" class="com.opensymphony.xwork2.validator.validators.StringLengthFieldValidator"/&gt;
    &lt;validator name="regex" class="com.opensymphony.xwork2.validator.validators.RegexFieldValidator"/&gt;
&lt;/validators&gt;</pre>
自己需要注册自己的Validator时，可以使用上述相似的内容，这个文件需要放在WEB-INF/classes目录下，文件的名字叫validators.xml。
一旦自己定义了validators.xml文件，系统就不会在加载默认的Validators文件，所以在Validators.xml中需要拷贝默认的内容。
## 5.3节：Validation与Intercepter

Validation使用名字叫做validator的Intercepter，在默认情况下，struts2已经定义了这个Intercepter，我们在不加声明的情况下就可以使用Validation了。
## 5.4节：使用Java Annotation配置校验

import com.opensymphony.xwork2.validator.annotations包提供了一些必要的Annotation用来配置校验信息。  
这些内容包括：  
枚举类型  
ValidatorType  
Field 校验字段  
Simple 校验其他  
Annotation（标注）类型  
Validation  
用来标记一个类需要被校验  
ConversionErrorFieldValidator  
字段转换出错  
DateRangeFieldValidator  
日期范围校验  
DoubleRangeFieldValidator  
Double类型范围校验  
EmailValidator  
Email地址校验  
ExpressionValidator  
使用一个OGNL表达式的校验，功能非常强大  
FieldExpressionValidator  
针对一个字段的使用OGNL表达式的校验  
IntRangeFieldValidator  
Int类型范围校验  
RegexFieldValidator  
正则表达式校验  
RequiredFieldValidator  
必填字段校验  
RequiredStringValidator  
必填String校验，  
StringLengthFieldValidator  
字符串长度校验  
UrlValidator  
URL校验  
Validations  
可以组合上述的各种校验类型以满足更多的需求。  
VisitorFieldValidator  
可以将Action中的对象的属性的校验方法定位到已经定义的对象原有的校验方法
CustomValidator  
ValidationParameter  
两个类一起完成自定义的校验
## 示例

<pre escaped="true" lang="java" line="1">package com.jpleasure;

import com.opensymphony.xwork2.ActionSupport;
import com.opensymphony.xwork2.validator.annotations.FieldExpressionValidator;
import com.opensymphony.xwork2.validator.annotations.RequiredFieldValidator;
import com.opensymphony.xwork2.validator.annotations.StringLengthFieldValidator;
import com.opensymphony.xwork2.validator.annotations.Validation;
import com.opensymphony.xwork2.validator.annotations.ValidatorType;

@Validation()
public class RegisterAction extends ActionSupport {
    private String name;
    private String password;
    private String rePassword;
    private String mail;
    private String description;

    public String getName() {
        return name;
    }

    @RequiredFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "name is required")
    public void setName(String name) {
        this.name = name;
    }

    public String getPassword() {
        return password;
    }

    @RequiredFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "password is required")
    @StringLengthFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "password must has proper legnth",
            minLength = "5", maxLength = "12")
    public void setPassword(String password) {
        this.password = password;
    }

    public String getRePassword() {
        return rePassword;
    }

    @RequiredFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true,
            message = "input password again please!")
    @StringLengthFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "password must has proper legnth",
            minLength = "5", maxLength = "12")
    @FieldExpressionValidator(expression = "password eq rePassword",
            message = "two password must match")
    public void setRePassword(String rePassword) {
        this.rePassword = rePassword;
    }

    public String getMail() {
        return mail;
    }

    @RequiredFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "mail is required")
    public void setMail(String mail) {
        this.mail = mail;
    }

    public String getDescription() {
        return description;
    }

    @RequiredFieldValidator(type = ValidatorType.FIELD,
            shortCircuit = true, message = "description is required")
    public void setDescription(String description) {
        this.description = description;
    }

    public String execute() throws Exception {

        return SUCCESS;
    }
}</pre>
## 5.5节：使用XML配置Validation

Xml配置文件与Action的关系为：  
SomeAction.java – SomeAction-validation.xml  
且与SomeAction.class处在相同的目录中。  
SimpleAction-validation.xml文件示例：
<pre escaped="true" lang="xml" line="1">&lt;!DOCTYPE validators PUBLIC "-//OpenSymphony Group//XWork Validator 1.0.2//EN"
       "http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd"&gt;
&lt;validators&gt;
  &lt;field name="bar"&gt;
      &lt;field-validator type="required"&gt;
          &lt;message&gt;You must enter a value for bar.&lt;/message&gt;
      &lt;/field-validator&gt;
      &lt;field-validator type="int"&gt;
          &lt;param name="min"&gt;6&lt;/param&gt;
          &lt;param name="max"&gt;10&lt;/param&gt;
          &lt;message&gt;
bar must be between ${min} and ${max}, current value is ${bar}.
&lt;/message&gt;
      &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;field name="bar2"&gt;
      &lt;field-validator type="regex"&gt;
          &lt;param name="regex"&gt;[0-9],[0-9]&lt;/param&gt;
          &lt;message&gt;
The value of bar2 must be in the format "x, y", where x and y are between 0 and 9
&lt;/message&gt;
     &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;field name="date"&gt;
      &lt;field-validator type="date"&gt;
          &lt;param name="min"&gt;12/22/2002&lt;/param&gt;
          &lt;param name="max"&gt;12/25/2002&lt;/param&gt;
          &lt;message&gt;The date must be between 12-22-2002 and 12-25-2002.&lt;/message&gt;
      &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;field name="foo"&gt;
      &lt;field-validator type="int"&gt;
          &lt;param name="min"&gt;0&lt;/param&gt;
          &lt;param name="max"&gt;100&lt;/param&gt;
          &lt;message key="foo.range"&gt;Could not find foo.range!&lt;/message&gt;
      &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;validator type="expression"&gt;
      &lt;param name="expression"&gt;foo lt bar &lt;/param&gt;
      &lt;message&gt;Foo must be greater than Bar. Foo = ${foo}, Bar = ${bar}.&lt;/message&gt;
  &lt;/validator&gt;
&lt;/validators&gt;</pre>
我们看看上面的配置文件，首先每一个validatior都必须有一个type属性，type属性的值为我们前面定义的validator的name。  
Message提供了校验出错的信息，message有一个属性key，通过可以可以找到i18n文件定义的内容，但是key并不是必须的。Message体内部的消息为默认消息，当i18n文件中不存在时表示该消息。消息中可以使用${}来引用被校验的对象例如：${foo}，${bar}
## 5.6节：Validator和Field Validator

Field Validator用来校验一个字段，例如：
<pre escaped="true" lang="xml" line="1">&lt;field name="email_address"&gt;
  &lt;field-validator type="required"&gt;
      &lt;message&gt;You cannot leave the email address field empty.&lt;/message&gt;
  &lt;/field-validator&gt;
  &lt;field-validator type="email"&gt;
      &lt;message&gt;The email address you entered is not valid.&lt;/message&gt;
  &lt;/field-validator&gt;
&lt;/field&gt;</pre>
Filed validator可以从filed集成字段名字，这样可以将摸个Field的所有的校验局限在一定的范围内。
使用Validator可以校验多个字段之间的关系，例如：
<pre escaped="true" lang="xml" line="1">&lt;validator type="expression&gt;
         &lt;param name="expression"&gt;foo gt bar&lt;/param&gt;
         &lt;message&gt;foo must be great than bar.&lt;/message&gt;
&lt;/validator&gt;</pre>
Validator也可以校验一个字段，例如：
<pre escaped="true" lang="xml" line="1">&lt;validator type="required"&gt;
        &lt;param name="fieldName"&gt;bar&lt;/param&gt;
        &lt;message&gt;You must enter a value for bar.&lt;/message&gt;
&lt;/validator&gt;</pre>
但是为了将一个字段的所有校验放在一起，我们倾向于尽量使用field validator
## 5.7节：短路（Short-Circuiting）

参看如下例子：
<pre escaped="true" lang="xml" line="1">&lt;!DOCTYPE validators PUBLIC
        "-//OpenSymphony Group//XWork Validator 1.0.2//EN"
        "http://www.opensymphony.com/xwork/xwork-validator-1.0.2.dtd"&gt;
&lt;validators&gt;
  &lt;!-- Field Validators for email field --&gt;
  &lt;field name="email"&gt;
      &lt;field-validator type="required" short-circuit="true"&gt;
          &lt;message&gt;You must enter a value for email.&lt;/message&gt;
      &lt;/field-validator&gt;
      &lt;field-validator type="email" short-circuit="true"&gt;
          &lt;message&gt;Not a valid e-mail.&lt;/message&gt;
      &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;!-- Field Validators for email2 field --&gt;
  &lt;field name="email2"&gt;
     &lt;field-validator type="required"&gt;
          &lt;message&gt;You must enter a value for email2.&lt;/message&gt;
      &lt;/field-validator&gt;
     &lt;field-validator type="email"&gt;
          &lt;message&gt;Not a valid e-mail2.&lt;/message&gt;
      &lt;/field-validator&gt;
  &lt;/field&gt;
  &lt;!-- Plain Validator 1 --&gt;
  &lt;validator type="expression"&gt;
      &lt;param name="expression"&gt;email.equals(email2)&lt;/param&gt;
      &lt;message&gt;Email not the same as email2&lt;/message&gt;
  &lt;/validator&gt;
  &lt;!-- Plain Validator 2 --&gt;
  &lt;validator type="expression" short-circuit="true"&gt;
      &lt;param name="expression"&gt;email.startsWith('mark')&lt;/param&gt;
      &lt;message&gt;Email does not start with mark&lt;/message&gt;
  &lt;/validator&gt;
&lt;/validators&gt;</pre>
校验的顺序：首先Validator，其次Field Validator，但是在Validator或者Field Validator执行的过程中，顺序按照xml文件中的定义。短路的意思是，一旦一个短路的校验出错，其余后续的校验将不再进行。例如上述的顺序是：
1）Plain Validator 1  
2）Plain Validator 2  
3）Field Validators for email field  
4）Field Validators for email2 field
由于Validator 2是短路的，一旦Validator 2校验出错，则email和email2都不会进入校验过程。
## 5.8节：validate方法

ActionSupport实现了Validatable接口，这个接口中定义了一个validate方法，通过重写validate方法可以完成更详细的校验，例如：
<pre escaped="true" lang="java" line="1">public void validate() {
  User user = getUser();
  if (StringUtils.isBlank(user.getName())) {
    addActionError(getText("user.name.empty"));
  }
  if (StringUtils.isBlank(user.getAddress())) {
    addActionError(getText("user.address.empty"));
  }
}</pre>
ActionSupport同时也实现了ValidationAware接口，该接口提供了addActionError等输出错误消息的方法。