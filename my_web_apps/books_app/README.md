Railsの教科書を参考（http://igarashikuniaki.net/rails_textbook/）

cloud9を利用


Ruby version 2.3.0  
Rails version 4.2.0.beta2  


[CRUDの基礎とindexアクション](http://igarashikuniaki.net/rails_textbook/crud.html)


# メモ


---

## scaffoldコマンド

g scaffoldコマンドは
* 新規作成(Create)
* 表示(Read)
* 更新(Update)
* 削除(Destroy)
の機能を一度に作れる。


四つの機能の頭文字をとって**CRUD**機能という。

---



---

## scaffoldコマンドが生成するもの

* route(invoke resource_route)
* controller(invoke scaffold_controller)
* view(invoke erb)

の他に、

画面がある

* index(一覧)
* new(新規入力)
* edit(編集)
* show(詳細)

を生成します。

---



---

index  
↓   新規入力  
new  
↓   新規登録  
create(画面なし)  
↓   redirect  
show  

---

index  
↓   編集  
edit  
↓  
update(画面なし)  
↓  
show

---

index  
↓   削除  
destroy(画面なし）  
↓   redirect  
indexに戻る  


---



---

## Roust対応表

Rails.application.routes.draw do

~

end

の間に書く。

---


---

## Controller

    class BooksController < ApplicationController
        ...
        def index
            @books = Book.all
        end
        
        ...
        
class BooksController < ApplicationControllerからendまでが、  
BooksControllerのコード。

def indexからendまでが、indexアクションになる。


処理は`@books = Book.all`の部分で、＠booksはインスタンス変数  
Bool.allはBookの全データが詰まった配列を取得すること。


ここでのインスタンス変数名は本のデータが一つでも、複数形にするのが  
慣習である。RailsやRubyでは変数の複数、単数の意識が大切である。


---


---

## View

    <% @books.each do |book| %>
      <tr>
        <td><%= book.title %></td>
        <td><%= book.memo %></td>
        <td><%= link_to 'Show', book %></td>
        <td><%= link_to 'Edit', edit_book_path(book) %></td>
        <td><%= link_to 'Destroy', book, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
    
表示は`<% @books.each do |book| %>`から`<% end %>`で行う。

@booksに二つのデータが入っていた場合、`@books.each`は全データを繰り返し処理を行う。  
1回目の実行で、変数book(`|book|`の部分)に1冊目のデータが格納され、したの処理が行われ、  
表示される。2回目では2冊目のデータが変数bookに同様に格納される。book


index.html.erbはHTMLのテンプレートファイルなので`<%  %>`で囲まれたRubyコードは  
HTMLとして、結果が表示される。


---