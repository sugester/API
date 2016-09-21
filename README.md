# Sugester API

Opis jak zintegrować własną aplikację lub serwis z systemem <http://sugester.pl/>


Dzięki API można z innych systemów dodawać posty/sugestie/błędy itp

## Spis treści
+ [API Token](#token)  
+ [Dodanie postu - przykłady wywołania](#examples)  
	+ Dodanie nowej sugestii
+ [Post - specyfikacja](#post)


<a name="token"/>
##API token

Kod autoryzacyjny API (`API_TOKEN`) należy pobrać z ustawień aplikacji w menu: Ustawienia > API > Kod autoryzacyjny API. Dzięku niemu w wywołaniach API nie trzeba będzie podawać swojego loginu/hasła.

<a name="examples"/>
##Przykłady wywołania

Dodanie nowego klienta:
```shell
curl http://sugester.sugester.dev/app/clients.json\
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "YOUR_API_TOKEN", 
"client": {
    "name":"client 1 from API",
    "email": "client1@emailexample1.net",
    "note": "note 1"    
  }
}'
```

Pobranie danych klienta:
```shell
curl http://sugester.sugester.dev/app/clients/7575347.json?api_token=YOUR_API_TOKEN
```

Aktualizacja danych klienta:
```shell
curl http://sugester.sugester.dev/app/clients/7575347.json\
     -X PUT \
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "YOUR_API_TOKEN", 
"client": {
    "note": "note from API"    
  }
}'
```

Usunięcie klienta:
```shell
curl -X DELETE  http://sugester.sugester.dev/app/clients/12345.json?api_token=YOUR_API_TOKEN
```

Dodanie nowego zadania:
```shell
curl http://sugester.sugester.dev/app/posts.json \
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "YOUR_API_TOKEN", 
"post": {
    "title":"task title 1 from API",
    "content": "task content 1",
    "task_kind": "task",
    "client_id": null,
    "responsible_id": 340507
  }
}'
```

Dodanie nowego dealu:
```shell
curl http://sugester.sugester.dev/app/deals.json\
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "YOUR_API_TOKEN", 
"deal": {
    "name":"deal 1 from API",
    "description": "desc 1",
    "client_id": null
  }
}'
```

Dodanie nowego konta:
```shell
curl http://sugester.sugester.dev/app/account.json \
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "YOUR_API_TOKEN", 
"account": {
    "prefix":"sugester2",
    "initial_module": "crm",
    "from_partner": "partner1"
 },
"user": {
    "login": "login1",
    "email": "email1@sugester-email.pl",
    "password": "password1"
 }
}'
```

Dodanie posta o typie "błąd":

```shell
curl http://your-prefix.sugester.pl/app/posts.json \
     -H 'Accept: application/json' \
     -H 'Content-Type: application/json' \
     -d '
{
"api_token": "API_TOKEN", 
"post": {
    "title":"post title2", 
    "content": "post content 2",
    "kind": "error"
  }
}'
```


<a name="post"/>
##Specyfikacja pól obiektu Post (Zadania/Sugestia/Zgłoszenie/E-mail)

```shell
{
    "id": id posta
    "title": tytuł 
    "content": treść
    "kind": rodzaj sugestii ('suggestion', 'error', 'question', 'praise', 'private'),
    "user_id": id usera
    "points": liczba punktów
    "nick": nick usera
    "votes_cache": ilość oddanych głosów
    "comments_cache": ilość oddanych komentarzy
    "forum_id": id forum
    "category_id": id category
    "created_at": czas utworzenia
    "updated_at": czas ostatniej modyfikacji
    "ip": ip z którego oddano post
    "agent": info o przeglądarce
    "response": odpowiedź główna
    "response_user_id": id osoby która odpowiedziała
    "referrer": refferer
    "responsible_id": id przypisanej osoby
    "last_action_status": status ("created"),
    "email": email nadawcy
    "uid": token użytkownika,
    "spam_kind": rodzaj spamu,
    "answer": odpowiedz,
    "answered": czy jest odpowiedz,
    "duplicate_from_id": id duplikatu,
    "abstract": abstrakt,
    "status_id": id status,
    "view_count": ilość wyświetleń,
    "tags": tagi,
    "facebook_likes": ilość like facebokoowych,
    "min_votes_to_start": ilość głosów do rozpoczęcia prac,
    "use_html": czy html,
    "email_to": adres email do,
    "email_cc": adres email cc,
    "email_bcc": adres email bcc,
    "spam_score": scoring spamowy,
    "spam_report": info o spamie,
    "closed": czy zamkniete (true/false),
    "scheduled_at": przypisana data wykonania,
    "task_kind": rodzaj zadania ('feedback', 'email', 'task', 'help', 'chat', 'phone', 'lead', 'error', 'idea'),
    "priority": priorytet,
    "title_note": null,
    "user_spam_report": zgłoszenie spamu,
    "client_id": id klienta,
    "project_id": id projektu,
    "help_link": klucz linka pomocy,
    "help_content": treść pomocy,
    "post_id": id postu nadrzędnego,
    "www": strona www dodajacego post,
    "private": czy prywatny (true/false),
    "unread": czy nie przeczytany (true/false),
    "email_recipient": do kogo jest dany post (uzywane w helpdesk/mail),
    "email_reply_to": reply to  (uzywane w helpdesk/mail)
}
```

