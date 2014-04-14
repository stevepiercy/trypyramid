===========
Use Pyramid
===========

Install
-------
If you don't have the latest and greatest Python 3 install it from `Python.org <https://www.python.org/downloads/>`_ 

In a terminal::

  $ pyvenv myproject
  $ cd myproject
  $ bin/pip install pyramid

Create Application
------------------

Open `app.py` in your editor::

  from pyramid.config import Configurator
  from pyramid.response import Response
  
  from wsgiref.simple_server import make_server
  
  def hello_world(request):
      return Response('Hello %(name)s!' % request.matchdict)
  
  def create_app():
      config = Configurator()
      config.add_route('hello', '/hello/{name}')
      config.add_view(hello_world, route_name='hello')
      app = config.make_wsgi_app()
      return app
  
  if __name__ == '__main__':
      app = create_app()
      server = make_server('0.0.0.0', 8080, app)
      server.serve_forever()