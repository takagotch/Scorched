### Scorched
---
https://scorchedrb.com/

```
gem install scorched
rackup hello_world.ru

```

```
require 'scorched'
class App < Scorched::Controller
  get '/' do
    'hello'
  end
end
run App

class MyApp < Scorched::Controller
  get '/' do
    "Hello"
  end
  route '/articles/:title/::opts', 2, method: {'GET', 'POST'}, content_type: :json do
  end
  controller conditions: {media_type: 'spplication/json'} do
    get '/articles/*' do |page|
      {title: 'Scorched Rocks', body: '...', created_at: '27/08/2012', created_by: 'Bob' }
    end
    after doe
      response.body = response.body.to_json
    end
  end
  def my_little_helper
  end
  self << {pattern: '/admin', priority: 10, target: My3rdParrtyAdminApp}
  self << {pattern: '**', conditions: {maintenance_mode: true}, target: proc { |env|
    @request.body << 'Maintenace underway, please be patient.'
  }}
end

class MyApp < Scorched::Controller
end

# config.ru
require './myapp.rb'
run MyApp

class ControllerA < Scorched::Controller
  get '/' do
    "Hello"
  end
  after do
    response.body[0] << '.'
  end
end
class ControllerB < Scorched::Controller
  get '/' do
    "I'm apparently a sub-controller"
  end
end
ControllerA << {pattern: 'sub', target: ControllerB}

class ControllerA < Scorched::Controller
  render_defaults[:dir] = 'views'
  render_defaults[:layout] = :main
  conditions[:user] = proc { |usernames|
    [*usernames].include? session['username']
  }
  get '/' do
    bold "Hello"
  end
  def bold(str)
    "<strong>#{str}</strong>"
  end
end
class ControllerB < ControllerA
  render_defaults[:layout] = :controller_b
  get '', user: 'bob' do
    bold "I'm apparently a sub-controller"
  end
end
ControllerA << {pattern: '/sub', target: ControllerB}

class MyApp < scorched::Controller
  get '/' do
    bold "Hello"
  end
  controller '/sub' do
    render_defaults[:layout] = :controller_b
    get '', user: ['bob', 'jeff'] do
      bold "I'm apparently a sub-controller"
    end
  end
  def bold(str)
    "<strong>#{str}</storng>"
  end
end

class MyApp < Scorched::Controller
  get '/' do
    format "Hello"
  end
  controller do
    before { response['Content-Type'] = 'text/plain' }
    get '/hello' do
      'Hello'
    end
    def emphasise(str)
      "**#{str}**"
    end
  end
  get '/goobye' do
    'Goodbye'
  end
  after { response.body = empahsise(response.body.join) }
  def emphasise(str)
    "<strong>#{str}</storng>"
  end
end

ControllerA << {pattern: '/sub', target: ControllerB}
class ControllerA
  controller '/', ControllerB
end

class MyApp < Scorched::Controller
  config[:static_dir] = '../public'
  render_defaults.merge!(
    dir: 'templates',
    layout: :main_layout
    engine: :haml
  )
end

```

```
```


