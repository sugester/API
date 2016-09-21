# Sugester API

Opis jak zintegrować własną aplikację lub serwis z systemem <http://sugester.pl/>


Dzięki API można z innych systemów dodawać posty/sugestie/błędy itp

## Spis treści
+ [API Token](#token)  
+ Przykłady wywołania
	+ [Dodanie klienta] (#client_create)
	+ [Pobranie danych klienta] (#client_show)
	+ [Aktualizacja danych klienta] (#client_update)
	+ [Skasowanie klienta] (#client_destroy)
	+ [Dodanie zadania] (#post_task_create)
	+ [Dodanie dealu] (#deal_create)
	+ [Dodanie nowej sugestii] (#post_error_create)
	+ [Dodanie konta partnerskiego] (#account_create)
+ [Klient - specyfikacja](#client)
+ [Post - specyfikacja](#post)


<a name="token"/>
##API token

Kod autoryzacyjny API (`API_TOKEN`) należy pobrać z ustawień aplikacji w menu: Ustawienia > API > Kod autoryzacyjny API. Dzięku niemu w wywołaniach API nie trzeba będzie podawać swojego loginu/hasła.

<a name="examples"/>
##Przykłady wywołania

<a name="client_create"/>
Dodanie nowego klienta:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/clients.json\
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

<a name="client_show"/>
Pobranie danych klienta:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/clients/1234.json?api_token=YOUR_API_TOKEN
```

<a name="client_update"/>
Aktualizacja danych klienta:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/clients/1234.json\
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

<a name="client_destroy"/>
Usunięcie klienta:
```shell
curl -X DELETE  http://YOUR-PREFIX.sugester.pl/app/clients/12345.json?api_token=YOUR_API_TOKEN
```

<a name="post_task_create"/>
Dodanie nowego zadania:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/posts.json \
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
    "responsible_id": 1234
  }
}'
```

<a name="deal_create"/>
Dodanie nowego dealu:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/deals.json\
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

<a name="post_error_create"/>
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

<a name="account_create"/>
Dodanie nowego konta:
```shell
curl http://YOUR-PREFIX.sugester.pl/app/account.json \
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

<a name="client"/>
##Specyfikacja pól Klienta 
```shell
{
	"id": id klienta
	"name": nazwa klienta
	"tax_no": numer nip
	"post_code": kod pocztowy
	"city": miejscowosc
	"street": ulica
	"first_name": imię
	"country": kraj
	"email": e-mail
	"phone": telefon
	"www": strona www
	"fax": fax
	"created_at": utworzenie 
	"updated_at": aktualizcja
	"street_no": ulica
	"kind": rodza ('buyer/seller')
	"bank": nazwa banku
	"bank_account": konto bankowe
	"bank_account_id": 
	"shortcut": skrót nazwy klienta
	"note": notatka
	"last_name": nazwisko
	"discount": zniżka
	"payment_to_kind": domyślny cza płatności faktury
	"use_delivery_address": adres korespondencyjny aktywny
	"delivery_address":  adres korespondencyjny
	"mobile_phone": telefon komórkowy
	"company": czy firma
	"register_number": numer regon
	"description": opis
	"project_id": id projektu
	"contact_id": id kontaktu głównego
	"appendixes_count": ilość załączników
	"posts_count": ilość emaili/zadań
	"contacts_count": ilość kontaktów
	"last_activity": ostatnia aktywność
	"string1..10": pola dodatkowe
	"integer1..10": pola dodatkowe
	"decimal1..10": pola dodatkowe
	"checkbox1..10": pola dodatkowe
	"date1..10": pola dodatkowe
	"text1..10": pola dodatkowe
	"datetime1..10": pola dodatkowe
	"avatar_file_name": avatar
	"avatar_content_type"
	"avatar_file_size"
	"avatar_updated_at"
	"status_id": id statusu
	"category_id": id kategorii
	"department_id": id departamentu
	"position": pozycja
	"creator_id": id osoby ktora dodala
	"updater_id": id osoby ktora ostatnio aktualizowala
	"responsible_id": id osoby odpowiedzialnej
	"province": wojewodztwo
	"sensitive_data": czy dane ukryte
	"external_id": ID klienta
	"token": token klienta
	"paid_from": od kiedy płatny
	"paid_to": do kiedy płatny
	"paid_total": suma płatności od klienta
}
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

