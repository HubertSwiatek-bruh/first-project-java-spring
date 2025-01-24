# Pierwsza aplikacja w springu - Case Study

## Opis

Aplikacja first-project-java-spring to prosta aplikacja webowa napisana w Javie na frameworku Spring Boot.

## Funkcjonalności

1. Defaultowy Endpoint "/":
   zwraca tekst: Hello Vistula, in my first Spring Controller :)
2. Endpoing Greeting: "/greeting"
   Generuje na podstawie parametru 'name' wiadomość zaadresowaną do osoby otwierającej stronę, wyświetla przykładowy tekst i obraz na stronie html z wykorzystaniem szablonów HTML ThymeLeaf
## Jak działa
  ### Kontroler 'HelloController' obsługuje żądania HTTP GET
  #### Dla "/"
    @GetMapping(value = "/")
    @ResponseBody
    public String hello(){
        return "Hello Vistula, in my first Spring Controller :)";
    }
  Wykorzystuje @ResponseBody aby wartość była zwracana jako treść odpowiedzi
  #### Dla "/greeting"
    @GetMapping ("/greeting")
    public String greeting(@RequestParam(name="name", required=false, defaultValue="World")String name, Model model){
        model.addAttribute("name", name);
        return "greeting";
  W tym przypadku aplikacja znajduje szablon o nazwie "greeting"
## Szablon HTML
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <meta http-equiv="Content-Type" content="text/html" charset="UTF-8"/>
    <title>Greeting Page Java Spring</title>
</head>
<body>
<p th:text="'Hello, ' + ${name} + '!'"/>
<p>
    Tekst typu przykładowy: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." itp itd. a niżej logo Springa
</p>
<img th:src="@{/SpringLogo.png}" width="800" height="800"/>
</body>
</html>
```
### Dynamicznie renderowany przez thymeleaf, 
th:text generuje dynamicznie wiadomość powitalną na podstawie parametru 'name'.

th:src wyświetla obraz na podstawie scieżki do zasobu statycznego.

## Przykład działania:

### Scenariusz użycia:
Użytkownik o imieniu "Hubert" wchodzi na '/greeting' z parametrem 'name': Hubert

localhost:8080/greeting?name=Hubert    - na potrzeby ćwiczenia robimy to przez localhost.

### Opis działania backendu:
1. 'greeting()' pobiera parametr 'name'
2. Obiekt Model przekazuje wartość parametru do szablonu
3. Plik 'greeting.html' jest renderowany z komunikatem dostosowanym do parametru, dodatkowym tekstem i obrazem.

### Wynik:
W przeglądarce wyświetlane są:
- Powitanie: "Hello, Hubert!"
- Dodatkowy tekst: "Tekst typu przykładowy: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." itp itd. a niżej logo Springa"
- Statyczny obraz: Obraz `SpringLogo.png` jest wyświetlany z podanymi wymiarami (800x800 pikseli).

![image](https://github.com/user-attachments/assets/e5b2bac6-7c20-4839-b42d-7ae29a258ca7)


## Podsumowanie:
Aplikacja jest prostym przykładem projektu w Spring Boot z dynamicznym renderowaniem HTML, wykonanym w ramach pracy domowej z zajęć "Programowanie - Java"
