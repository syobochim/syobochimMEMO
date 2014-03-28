============
rubyMEMO
============

.. contents:: 目次
   :depth: 3


はじめに
============

| このページは、 `dotinstall <http://dotinstall.com/>`_ のRuby on Rails 4 入門でやっていることを
| つらつらとメモしたものです。


アプリケーションの始め方
============

| myappというアプリケーションを始める。

::

  $ rails new myapp


| ↑のコマンドで、自動で必要なフォルダを作成してくれる。
| 作成されたフォルダに移動後、

::

  $ rails s


| でサーバーを起動。
| s は **s** erver の意味。
| JavaScriptランタイムエラーが発生したら、Gemfileを修正する必要がある
| 一回サーバを停止して(Ctrl + c)
| Gemfileを開いて、


::

  gem 'therubyracer', platforms: ruby


| のコメントアウトを外す。
|

::

  bundle install

| で必要なものをダウンロードして、
| 再度

::

  $ rails s


| をして、
| http://localhost:3000
| にアクセスできたらOK



Scafoldしよう！
============

| **Scafold** 　…　シンプルなアプリケーションの枠組みを作ってくれる
|

::

  $ rails generate scaffold users name:string score:integer

| で、Userっていうインスタンスに、
| string 型の name と integer 型の score というデータを作成してくれる。
|
| scaffold ができたら、DBにデータをマイグレーションする。
|

::

  $ rake db:migrate

| でマイグレーションは簡単！

|
| http://localhost:3000/users
| にアクセスすると、DBへのデータ登録・編集・削除を行うことが出来るアプリケーションが出来てる！


.. note::

  マイグレーションとは、プログラムやデータの移行・変換作業のこと。



タスク管理アプリを作ってみよう
============

| 新しいアプリケーションを作る。
| すでにbundle installが済んでいる場合は、
| bundle install をスキップすることができる。

::

  rails new taskapp --skip-bundle

| taskappというアプリケーションが作成される。
| あとは、アプリケーションの始め方に書いてあるように、
| ディレクトリ移動後にGemfile の修正を行う。


Modelを作ろう！
=============

| アプリケーションはModelからつくっていく。

|
| MVC(Model-View-Controle) とは、
| **Model**    ... データを管理するもの
| **View**     ... 画面
| **Controle** ... Model と Controle を操るもの
|
| Modelを作るコマンドは、

::

  $ rails generate model Project title:String

| ただし、generate は **g** に省力することができるし、
| 項目の作成もデフォルトはstring型に設定されているので、

::

  $ rails g model Project title

| と省略することができる。
| このコマンドを打つことで、さらにファイルが作成される。

.. warning::

  **命名規則：** Model 名は、最初の１文字にして、単数系にすること！


| そのあとは、

::

  $ rake db:migtate

| すれば、DBへの適用はOK！！


rails db/ rails console を使おう！
=============

ターミナルで、

::

  rails db

| を入力すると、現在つながっているDBへ接続することができる！
| MySQLに接続するために、
| config/databese.ymlを下記のように書き換えた。

::

  development:
    adapter: mysql2
    encoding: utf8
    database: sample_development
    pool: 5
    username: root
    password:
    socket: /tmp/mysql.sock
    
  test:
    adapter: mysql2
    encoding: utf8
    database: sample_test
    pool: 5
    username: root
    password:
    socket: /tmp/mysql.sock

  production:
    adapter: mysql2
    encoding: utf8
    database: sample_production
    pool: 5
    username: root
    password:
    socket: /tmp/mysql.sock


| socketは個人個人で違う？
| mysqlが入ってるところかな？
| これを設定した後は、改めて

::

  rake db:create

| をしないといけなかった。

.. image:: ./img/rails_db.png

| できた！
|
| rails console では、モデルをインタラクティブにいじれる！
| ターミナル上で、

::

  rails console


.. image:: ./img/rails_console.png


| この、rails consoleにて、DBへのデータ入力等ができる

::

  p = Project.new(title: "p1")

| で、titleにp1って入ったものができる。

::

  p.save

| で、DBへ保存！

::

  p

| で、実際にい入ったデータをみることができる
| 宣言とsaveの2つを合わせたコマンドが↓

::

  Project.create(title: "p2")

| すべてのデータをみるのは、↓

::

  Project.all


| rails db を起動して、データをみたら、いい感じに入っているのが確認できる

.. image :: ./img/rails_db2.png


| みんなでデータを共有するときは、
| db/seeds.rb ファイルにデータを書いていけばいい！
| 参考：http://www.rubylife.jp/rails/model/index10.html
|
| 適用するときは、

::

  rake db:seed

| を使用する！
|
| dbを削除するときは

::

  rake db:drop


Controller を作ろう！
=============

controlleer を作成するコマンド

::

  $ rails g controller Projects

で、Projectsっていうコントローラーができる

.. warning::

  命名規則：Contoroller の命名は、最初の１文字が大文字の複数系にすること！

| コントローラーが作成できたら、
| config/routes.rb を編集する。

::

  Taskapp::Application.routes.draw do
    resources :projects
  end

| コメントアウトした部分を除いて、↑みたいな感じにする
|
| コマンドにて、

::

  rake routes

| をすると、routeの確認ができる。

.. image:: ./img/rake_routes.png



Project の一覧を表示させる
==============

.. image:: ./img/Project_all.png

| ↑より、indexというものでプロジェクトの一覧を作ることができることを読み解く！
| (...?)
|
| app/controllers/projets_controllers.rb
| を開いて、indexアクションを作っていく！

.. code-block:: ruby

  class ProjectsController < ApplicationController

    def index
      @projects = Project.all
    end

  end

| index アクションを作成できたら、
| それを表示するViewをつくる！
| app/views/projects  フォルダに、ファイルを新規作成する。
| 今回は、indexのViewをつくるので、
| ファイル名は、index.html.erbにした。

.. warning::

  命名規則：View名は、Controllerで宣言した名前と合わせること！


| ファイルの中身はこんな感じ


.. code-block:: ruby

  <h1>Projects</h1>

  <ul>
      <% @projects.each do |project| %>
      <li><%= project.title %></li>
      <% end %>
  </ul>


| <% %> の中に、処理を書く。
| <%= %>の中に、値を書く。

.. image:: ./img/Project_all.png

| ↑より、/projectsでindexにアクセスすることがわかるので、
| サーバーを起動($ rails s)して、
| http://localhost:3000/projects
| にアクセスすると、登録したタイトルが表示される。

.. image:: ./img/index.png


rootの設定をしよう
==============

| rootingを設定していく。

.. note::

   rootingとは、URLとアクションを関連づけるもの

|
| http://localhost:3000/projects  を
| http://localhost:3000/  のURLでアクセスできるように設定していく。
|
| config/routes.rb ファイルを開く
|

.. code-block:: ruby

  root 'projects#index'

| を追加すると、
| http://localhost:3000/projects  の画面に、
| http://localhost:3000/  のURLでアクセスできるようになった！
|

.. note::

   rootは大元って意味。

.. note::

   他にも、いろいろな設定がコメントアウトされて載っている。
   rootingの設定を変えたいときは参考にすること。


共通テンプレートを編集しよう！
================

| 共通のテンプレートの編集方法
| app/views/layouts/applocation.html.erb
| ファイルを編集して、共通テンプレートを変えていく

.. code-block:: ruby

  <%= yield %>

| に、それぞれのviewで書いたものが挿入されていく
|
| image の挿入方法

.. code-block:: ruby

   <%= image_tag "logo.png" %>

| logo.png は、app/assert/images フォルダ内に格納すること。
|
| link の挿入方法

.. code-block:: ruby

  <%= link_to "Home", "/" %>

| Homeって文字がリンクになった、root (localhost:3000)へのリンクができる。
|
| これは、

.. code-block:: ruby

  <%= link_to "Home", projects_path %>

| ってやってもOK。
| projects_pathについては、

.. image:: ./img/rake_routes2.png

| で、矢印が指している箇所の後に「_path」をつけると、
| そのURIの場所に飛ぶようになっている！
|
| 共通のimg / JavaScript / CSS は、
| app/assert/ フォルダの下で定めている。


詳細画面を作ろう！
============

.. image:: ./img/rake_routes_show.png

| 名前：project
| 作成するページのURL ：/projects/:id
| URLに取ってくる値：id
| View名：show
|
| で、ページを作る！
|
| まずは、Controllerを編集する
| project_controller.rb に下記を追加する

.. code-block:: ruby

    def show
      @project = Project.find(params[:id])
    end

|
| app/views/projects フォルダに移動して、
| index.html.erb に、詳細ページへのリンクを作成する
| <li>の中身をリンクにするので、↓みたいに書き換えていく

.. code-block:: ruby

   <li><%= link_to project.title, project_path(project.id) %></li>

| link_to でリンク作成
| project.title がリンクにされる文字
| project_path で遷移先を指定 (rake routes の project で定めている箇所に遷移)
| 遷移先への引数は id
|
| show.html.erb ファイルを作成して、
| 詳細画面の中身を書いていく

.. code-block:: ruby

   <h1><%= @project.title %></h1>


| こんな画面ができる！
|
| **index**

.. image:: ./img/link_index.png

| **詳細ページ**

.. image:: ./img/detail.png


新規作成フォームを作ろう！
=============

| 新しいProjectを作成するページを作成していく
|
| **全体の流れ**

.. image:: ./img/rake_routes_new.png

| new ページに新規登録するためのフォームを作成して、

.. image:: ./img/rake_routes_create.png

| create でデータを登録する！
|
| **では、やっていきましょう！**
| index.html.erb に、new 画面へのリンクを作成する

.. code-block:: ruby

  <h1>Projects</h1>

  <ul>
    <% @projects.each do |project| %>
         <li><%= link_to project.title, project_pathoject.id) %></li>
    <% end %>
  </ul>

  <p><%= link_to "Add New", new_project_path %></p>

| リンクが出来たら、Controllerを追加していく
| projects_controller.rb
| に下記を追加。

.. code-block:: ruby

   def new
     @project = Project.new
   end

| Actionができたら、Viewを作成する。
| new.html.erb ファイルを作成したら、
| 中身を書いていく

.. code-block:: ruby

   <h1>Add new</h1>

   <%= form_for @project do |f| %>

   <p>
     <%= f.label :title %>
     <%= f.text_field :title %>
   </P>

   <p>
     <%= f.submit %>
   </p>

   <% end %>

| label ... ラベル
| text_field ... テキストボックス
| submit ...サブミットボタン
|
| これで、↓の画面ができる！

.. image:: ./img/new_page.png


データを保存してみよう！
=============

| ↑で作成したフォームに入力した値をPOSTで登録していく！

.. image:: ./img/rake_routes_create.png

| ControllerにActionを追加

.. code-block:: ruby

    def create
      @project = Project.new(project_params)
      @project.save
      redirect_to projects_path
    end

    private

      def project_params
        params[:project].permit(:title)
      end

|
| project_param は下の def で定義している。
| フォームからPOSTでわたされたものはprivate内で改めて定義する必要がある。
| (セキュリティ上、フィルタリングをする必要がある。)
| redirect_to でページ遷移


Validationを設定しよう！
================

| ↑で情報の登録機能を作成したが、
| 今の状態では入力値が何もなくても登録できてしまう。
| そのため、精査機能(Validationn)を作成して、
| データの入力を規制する。
|
| app/models/project.rb ファイルにValidationの設定を書いていく

.. code-block:: ruby

   class Project < ActiveRecord::Base
     validates :title, presence: true
   end

| title にValidationをつける。
| presence は、入力必須精査って意味。
| これをtrueにすることで、titleが空のときは精査ではじく処理を定義。
|
| このままでは、newページの入力値が空な場合でも、
| プロジェクト一覧ページに遷移してしまうので、
| 精査エラーのときはnewページのまま遷移しないように設定する必要がある。
| projects_controller.rb を編集していく

.. code-block:: ruby

    def create
      @project = Project.new(project_params)
      if @project.save
        redirect_to projects_path
      else
       render 'new'
      end
    end


.. note::

   @project.save はboolean型なので、if分の条件分岐に使用することができる


| render で 遷移先を new ページと定義
|

render と redirect_to の違い
----------------

| **render** はViewを指定する。
| エラーメッセージ表示のために、元の画面に差し戻す際などに利用する。
|
| **redirect_to** はリダイレクトによる処理の委譲をする。
| リクエストを別のアクションに委譲する。


エラーメッセージを表示しよう
=================

| 精査エラーが発生したときのエラーメッセージ
をnewページに表示させる。
|
| new.html.erb ファイルを編集する。

.. code-block:: ruby

    <% if @project.errors.any? %>
    <%= @project.errors.inspect %>
    <% end %>

| ↑を追記。
| errors.inspect でエラーの内容を表示することができる。
| 精査エラーとなる値(今回は空文字)を入力してサブミットすると、
|

.. image:: ./img/error_inspect.png

| とエラー内容が表示される。
| エラー内容をみると、 message には、title 項目に配列型で値が格納されていることが読み取れる。
| なので、new.html.erb ファイルの追加した部分を↓のように変える。

.. code-block:: ruby

    <% if @project.errors.any? %>
    <%= @project.errors.messages[:title][0] %>
    <% end %>

| すると、エラーメッセージが下記のように表示される。

.. image:: ./img/error_msg1.png

|
| 任意の値にエラーメッセージを変更することも可能。
| project.rb にエラーメッセージを定義していく。
|
| 先ほど追加した箇所を下のように変更

.. code-block:: ruby

   class Project < ActiveRecord::Base
     validates :title, presence: { message: "入力してください。" }
   end

| これで、エラーメッセージが変わった。

.. image:: ./img/error_msg2.png

|
| ほかにも、さまざまな精査を追加することができる
|
| たとえば、3文字以上でないと精査エラーになるとしたければ、
| 下記のようにかく。

.. code-block:: ruby

   class Project < ActiveRecord::Base
     validates :title,
       presence: { message: "入力してください。" },
       length: { minimum: 3, message: "短すぎ！" }
   end


編集フォームを作ろう
================

| 編集は、edit と update を使用する

.. image:: ./img/rake_routes_edit.png

| view を編集していく
| idex.html.erb を下のように書き換える（liタグの中身を編集）

.. code-block:: ruby

   <h1>Projects</h1>
  
   <ul>
         <% @projects.each do |project| %>
           <li>
             <%= link_to project.title, project_path(project.id) %>
             <%= link_to "[Edit]", edit_project_path(project.id) %>
           </li>
         <% end %>
   </ul>

   <p><%= link_to "Add New", new_project_path %></p>

| すると、↓みたいになる。

.. image:: ./img/index_edit.png

| ページが出来たら Action を作る！
| project_controller.rb を開いて、
| 下記を追加する

.. code-block:: ruby

    def edit
      @project = Project.find(params[:id])
    end

| そのあと、Viewを作成していく。
| edit.html.erb を作成する。
| new.html.erb をコピーして、タイトル(h1タグ内)をEdit等に変えればとりあえずOK！
|
| ページは↓のようになる。

.. image:: ./img/view_edit.png

| 矢印が指しているボタンを見ると、
| new ページのときはCreateだったのに、
| edit ページではUpdateになっている！
| かしこい！！


データを更新しよう
=================

| Controller に update アクションを作成する

.. code-block:: ruby

    def update
      @project = Project.find(params[:id])
      if @project.update(project_params)
        redirect_to projects_path
      else
        render 'edit'
      end
    end

| これで、先ほどのEdit画面のフォームに入力した値を反映させることができる。
| また、設定した精査エラーに関しても、同じように出力される！
|

DRY をわすれるな！
-------------

| **しかし！**
| new ページと Edit ページの内容が、ほぼほぼ同じになっているのは、
| DRYの精神に反している！！

.. note::

   DRY ... Don't repeat yourself 　同じことを繰り返すな！

| 共通部分の下記を、/app/views/projects フォルダ内に
| **_** form.html.erb　というファイルを作って切り出す！

.. warning::

   共通部分のファイル名は、先頭にアンダーバー(_)をつけること！

|
| 今回は、下記の部分を切り出した。

.. code-block:: ruby

   <%= form_for @project do |f| %>

   <p>
     <%= f.label :title %>
     <%= f.text_field :title %>
     <% if @project.errors.any? %>
     <%= @project.errors.messages[:title][0] %>
     <% end %>
   </P>

   <p>
     <%= f.submit %>
   </p>

   <% end %>

| 切り出した後の new , edit は、↓みたいな感じ。
|

.. code-block:: ruby

   <h1>Add new</h1>

   <%= render 'form' %>

| **シンプル！！**
|
| render に指定した、form と、 _form.html.erb がリンクしている！


データを削除しよう！
=============

.. image:: ./img/rake_routes_destroy.png

| Actionクラスはdestroy!!
| まずはリンクを作成する
| index.html.erb ファイルに下記を追加。
| Editボタンの下に追記しました。

.. code-block:: ruby

   <%= link_to "[Delete]", project_path(project.id), method: :delete, data: { confirm: "are you sure?" } %>

| delete メソッドの呼び出しを行う。
| 確認(confirm)メッセージとして、「are you sure?」を設定。
|
| 次にActionを書いていく
| projects_controller.rb に追記

.. code-block:: ruby

    def destroy
      @project = Project.find(params[:id])
      @project.destroy
      redirect_to projects_path
    end

| これで、index ページにあるデータを消していくことができる！

.. image:: ./img/index_delete.png


before_action を使ってみよう
=================

| ここまでで、Controller いろいろと書いてきたが
| DRYになっていない箇所がいくつかある！

.. code-block:: ruby

   class ProjectsController < ApplicationController

      def index
        @projects = Project.all
      end

      def show
        @project = Project.find(params[:id])
      end

      def new
        @project = Project.new
      end

      def create
        @project = Project.new(project_params)
        if @project.save
          redirect_to projects_path
        else
          render 'new'
        end
      end

      def edit
        @project = Project.find(params[:id])
      end

      def update
        @project = Project.find(params[:id])
        if @project.update(project_params)
          redirect_to projects_path
        else
          render 'edit'
        end
      end

      def destroy
        @project = Project.find(params[:id])
        @project.destroy
        redirect_to projects_path
      end

      private

        def project_params
          params[:project].permit(:title)
        end
    end

| @project = Project.find(params[:id]) の部分が何度も出てきている！
| 同じ記述は切り出す！！

.. note::

   before_action は、すべてのメソッドの最初に実行。
   after_action は、すべてのメソッドの最後に実行。

| 今回、@project = Project.find(params[:id]) が出てくるのは、
| show, edit, update, destroy だけなので、only でメソッドで、実行メソッドを指定する。
| 処理はprivate内に記載。

.. code-block:: ruby

   class ProjectsController < ApplicationController

      before_action :set_project, only: [:show, :edit, :update, :destroy]

      def index
        @projects = Project.all
      end

      def show
      end

      def new
        @project = Project.new
      end

      def create
        @project = Project.new(project_params)
        if @project.save
          redirect_to projects_path
        else
          render 'new'
        end
      end

      def edit
      end

      def update
        if @project.update(project_params)
          redirect_to projects_path
        else
          render 'edit'
        end
      end

      def destroy
        @project.destroy
        redirect_to projects_path
      end

      private

        def project_params
          params[:project].permit(:title)
        end

        def set_project
          @project = Project.find(params[:id])
        end
    end

| すっきり！


Taskの設定をしていこう！
==============

| Project の詳細ページにTask機能を追加していきましょう！
|
| 新しくTaskアプリを作成する。

::

  $ rails g model Task title done:boolean project:references

| で、新しく Model を作成する。
| project:references で、事前に作っている project と関連付けさせることができる。
|
| done (Taskを実施したか) は、最初はfalseに設定しておく。
| db/migrate/xxxx_create_tasks.rb
| ファイルを編集する。

.. code-block:: ruby

    class CreateTasks < ActiveRecord::Migration
      def change
        create_table :tasks do |t|
          t.string :title
          t.boolean :done, default: false
          t.references :project, index: true

          t.timestamps
        end
      end
    end


| default: false
| を追加した。
|
| 編集後に

::

  rake db:migrate

| した後、Controllerを作成すれば準備OK！

::

  rails g controller Tasks


Association の設定をしよう
================

| app/models フォルダの中に、

- task.rb
- project.rb

| ファイルがある。
| task.rb ファイルの中をみると、

.. code-block:: ruby

   class Task < ActiveRecord::Base
     belongs_to :project
   end

| project が結び付けられているのがわかる
|
| project.rb には、task と project の関連付けができていないので

.. code-block:: ruby

   has_many :tasks

| を追記する。
| has_many は、Project１つに対して、Taskが複数あるという意味。(1 対 多)
|
| 続いて、routing を関連付けていく
| config/routes.rb ファイルを編集する。
| 下記の記述を追記。

.. code-block:: ruby

   resources :projects do
     resources :tasks, only: [:create, :destroy]
   end

| Taskの機能は生成と削除だけでいいので、
| create と destroy 機能のみをつける
|
| これで、

::

  $ rake routes

| すると、↓みたいにtasksの項目が追加されていることがわかる。

.. image:: ./img/rake_routes_task.png


Tasksの新規作成フォームを作ろう
=============

| server を起動した後、
| app/views/projects フォルダ内の show.html.erb ファイルを編集して、
| ページを作る。

.. code-block:: ruby

   <h1><%= @project.title %></h1>

   <ul>
     <% @project.tasks.each do |task| %>
     <li>
       <%= task.title %>
     </li>
   <% end %>
   <li>
     <%= form_for [@project, @project.tasks.build] do |f| %>
      <%= f.text_field :title %>
      <%= f.submit %>
      <% end %>
    </li>
    </ul>

| project と task が結びついているので、@project.tasks で値をとることができる
| form_for のところの[@project, @project.tasks.build] は決まり文句。
| project と task を関連付けてデータを作成してくれる。

.. image:: ./img/view_task.png


Tasks を保存しよう！
===============

| Controller を作成する
| app/controllers/tasks_controller.rb を開く

.. code-block:: ruby

    class TasksController < ApplicationController
      def create
        @project = Project.find(params[:project_id])
        @task = @project.tasks.create(task_params)
        redirect_to project_path(@project.id)
      end

      private

        def task_params
          params[:task].permit(:title)
        end

    end

| project で作ったのとおんなじ感じ
|
| validationを定める
| app/models/task.rb

.. code-block:: ruby

   class Task < ActiveRecord::Base
     belongs_to :project
       validates :title, presence: true
   end

| これで作成機能はつくれる！


Tasks の削除をする
==============

| Taskの削除機能を作成する
| app/views/projects/show.html.erb に削除リンクを追加する。
|

.. image:: ./img/rake_routes_task_destroy.png

| より、tasks#destroy は
| taskの :project_id と :id が必要であることがわかる。
| 遷移させるpath は project_task 。
| よって、show.html.erb は下記のようになる。



.. code-block:: ruby

   <h1><%= @project.title %></h1>

   <ul>
     <% @project.tasks.each do |task| %>
     <li>
       <%= task.title %>
       <%= link_to "[Delete]", project_task_path(task.project_id, task.id), method: :delete, data: { confirm: "are you sure?" } %>
      </li>
    <% end %>
    <li>
      <%= form_for [@project, @project.tasks.build] do |f| %>
      <%= f.text_field :title %>
      <%= f.submit %>
      <% end %>
    </li>
   </ul>

| また、app/controllers/task_controller.rb には、下記を追加する。

.. code-block:: ruby

   def destroy
     @task = Task.find(params[:id])
     @task.destroy
     redirect_to project_path(params[:project_id])
   end

| rails routesにて destroy した際に id が返却されることがわかるので、
| find の引数は :id !


ceck_box_tagを使おう！
==============

| Taskを管理するためのチェックボックスを作ろう！
| show.html.erb にcheck_box_tag部分を追加

.. code-block:: ruby

   <h1><%= @project.title %></h1>

   <ul>
     <% @project.tasks.each do |task| %>
     <li>
       <%= check_box_tag '', '', task.done, {'data-id' => task.id, 'data-project_id' => task.project_id} %>
       <%= task.title %>
       <%= link_to "[Delete]", project_task_path(task.project_id, task.id), method: :delete, data: { confirm: "are you sure?" } %>
     </li>
   <% end %>
   <li>
     <%= form_for [@project, @project.tasks.build] do |f| %>
     <%= f.text_field :title %>
     <%= f.submit %>
     <% end %>
   </li>
   </ul>

.. note::

   check_box_tag 要素名, 値, checked = false, {その他設定したい値}


| 今回は name, valueは空。checkedにはtask.doneをそのまま適用。
| data-id には task.id、data-project_id にはtask.project_idを適用。
| 実際に生成されたHTMLは下記のようになる

::

  <index data-id="2" data-project_id= "1" id="" name="" type="checkbox" value="" />


| このあと、data-id と data-project_id を使用して、jQuery で Ajaxをなげる処理を作成していく！

toggle アクションを作ろう
=============

| チェックボックスをクリックしたときに
| Actionを動作させるようにする。
| show.html.erbの一番下に下記を追加する。

.. code-block:: html

   <script>
   $(function() {
       $("input[type=checkbox]").click(function() {
         $.post('/projects/'+$(this).data('project_id')+'/tasks/'+$(this).data('id')+'/toggle');
       });
   });
   </script>

| このjQueryで、POST形式の /project/:project_id/tasks/:id/toggle パスでActionが投げられる。
|
| ↑のパスをroutesに定義する。
| config/routes.rb に下記を追加する。

.. code-block:: ruby

   post '/projects/:project_id/tasks/:id/toggle' => 'tasks#toggle'

| rake routes すると、↓みたいに新しくroutesが追加されている。

.. image:: ./img/rake_routes_toggle.png

| routes が出来たら、Controllerを作成する。
|
| app/controllers/tasks_controller.rb
| に下記を追加する

.. code-block:: ruby

   def toggle
     render nothing: true
     @task = Task.find(params[:id])
     @task.done = !@task.done
     @task.save
   end

| render nothing:true はテンプレートを使用しないって意味。
| (toggleはページ遷移しないため、テンプレートは不要。)
| @task.done = !@task.done
| で、真偽値の値を逆にする。
|

.. note::

   何か問題がある場合は、JavaScriptコンソール(ブラウザにてF12して出てくる)でエラーが出る。


Task数を表示させよう
=============

| プロジェクト一覧にタスクの一覧を表示させる。
|
| app/views/projects/index.html.erb
| に残りのタスク数を表示させる。

.. code-block:: ruby

   <h1>Projects</h1>

   <ul>
         <% @projects.each do |project| %>
           <li>
           <%= link_to project.title, project_path(project.id) %> (<%= project.tasks.count %>)
             <%= link_to "[Edit]", edit_project_path(project.id) %>
             <%= link_to "[Delete]", project_path(project.id), method: :delete, data: { confirm: "are you sure?" } %>
           </li>
         <% end %>
   </ul>

   <p><%= link_to "Add New", new_project_path %></p>


| (<%= project.tasks.count %>) の部分を追加することで、

.. image:: ./img/index_task.png

| みたいに、全てのタスク数が表示される！
|
| 残りのタスク数を表示するには、modelに検索条件を追加すれば良い

.. code-block:: ruby

   scope :unfinished, -> { where(done: false) }

| これで、done が false のやつを数えてくれる。
|
|

.. code-block:: ruby

   <h1>Projects</h1>

   <ul>
         <% @projects.each do |project| %>
           <li>
           <%= link_to project.title, project_path(project.id) %> (<%= project.tasks.unfinished.count %>/<%= project.tasks.count %>)

             <%= link_to "[Edit]", edit_project_path(project.id) %>
             <%= link_to "[Delete]", project_path(project.id), method: :delete, data: { confirm: "are you sure?" } %>
           </li>
         <% end %>
   </ul>

   <p><%= link_to "Add New", new_project_path %></p>


| <%= project.tasks.unfinished.count %> で done が false のTasks数を表示。
|
| 結果は↓みたいな感じになる。

.. image:: ./img/index_tasks.png

| これで終わり！！！