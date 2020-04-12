# app
frontend React + backend Ruby on Rails


◆フロント
```
npx create-react-app frontend-react
yarn start
```


◆バックエンド
```
bundle init
vi Gemfile（コメントアウト gem "rails"）
bundle install --path vendor/bundle
bundle exec rails new backend-rails --database=postgresql --skip-bundle --api
```

```
cd backend-rails
vi Gemfile (コメントアウト　gem 'rack-cors')
bundle install --path vendor/bundle（gem install pg が失敗した ruby.nixにpostgresがないとそうなる。）
bundle exec rails db:create（フォルダ名[config/database.ymlに記載]でDBを作成する）
```

・ルートを追加
  config/routes.rb
```
Rails.application.routes.draw do
  get "hello_world", to: 'application#hello_world'
end
```

・hello_worldメソッドを追加
  app/controllers/application_controller.rb
```
class ApplicationController < ActionController::API
  def hello_world
    render json: { text: "Hello World" }
  end
end
```

・フロントからのアクセスを許可
  config/initializers/cors.rb
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins 'example.com'
#    origins /localhost\:\d+/

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```
