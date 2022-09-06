# flask-N12-custom-error-page
因为自带的报错页面很难看，所以我们自己建立一个报错页。比较简单

1. 由于是个与众不同的界面，所以把内容放在另一个folder里，叫errors：
里面有初始页 + handlers（处理器）
  
  handlers.py
    
          from flask import Blueprint, render_template
          放进已经分类好的蓝本 + 引用template-待会的html

          errors = Blueprint('errors', __name__)
          蓝本的初始定义


          @errors.app_errorhandler(404)
          怎么处理这些常见的问题页？把它们引到相应的html
          def error_404(error):
              return render_template('errors/404.html'),404

          @errors.app_errorhandler(403)
          def error_403(error):
              return render_template('errors/403.html'),403

          @errors.app_errorhandler(500)
          def error_500(error):
              return render_template('errors/500.html'),500

2. 主 __init__.py

           在create.app下面带进去，毕竟新folder
           注意.errors.handlers
           from flaskblog.errors.handlers import errors
           
           蓝本有：
           app.register_blueprint(errors)


3. 403.html等定义错误页面
注意，所有的errors页面放在template项下单独folder，这样就不会搞错了

          {% extends "layout.html" %} 
          {% block content %} 页面的复制模式
              <div class="content-section">
                  <h1>You don't have permission to do this. (403)</h1>
                  <p>Please caheck your account and try again.</p>
              </div>
          {% endblock content%}
