---
title: Les 6
layout: page
permalink: :path/:basename
nav_exclude: true
---

## Weergave van één project
{: .text-green-100 .fs-6 }

Je hebt een overzicht van de projecten gemaakt, nu gaan wij aan de slag om één project op te halen.


---
### 1- Route aanmaken
Wij beginnen met het aanmaken van een route met daarin een referentie naar het project Model. 

Open `/routes/web.php` en voeg daar een nieuwe route toe waarbij je in het url gedeelte op de laatste plek aangeeft dat er een verplichte variabele is.  
Dat doe je door de model naam tussen brackets te plaatsen:  
```php
Route::get('/project/{project}', [ProjectController::class, 'show'])->name('project.show');
```

---
### 2- Functie in de controller maken
Nu kun je deze route opvangen in de controller, je hebt aangegeven dat hij naar de `show` functie verwijst. Die maken wij nu aan.  
Let hierbij op dat je een parameter aanmaakt met dezelfde naam als de variabele in de route. In ons geval `project`.  
Maak ook gebruik van **type-casting** waarbij je forceert dat de variabele een Project is.  
```php
public function show(Project $project): string
{
}
```
Plaats in deze functie nu om te testen een debug code: `dump($project);`   
Hierdoor zie je in iedergeval iets als je naar de url gaat.

---
### 3- View
Kopieer nu de project index view en noem die sow.blade.php
Verwijder de loop en laat bijvoorbeeld de titel zien van het project:
{% raw %}
```php
<h2>{{$project->title}}</h2>
```
{% endraw %}


---
### 4- stuur het project door naar de view
Ga nu weer terug naar de **show** functie in de **ProjectController**.  
Geef daar nu het project door aan de view zoels in dit voorbeeld met een model. Dit zal voor jullie een project zijn.  
```php
    /**
     * Show a single item
     * 
     * @param Model $model
     * @return string
     */
    public function show(Model $model): string
    {
        return view('model.show', ['model'=>$model]);
    }
```


--- 
### 5- Link naar de show pagina
Nu heb je de single pagina gemaakt en moeten wij alleen nog een link maken naar deze pagina.  
Ga naar het **index** document waar je het overzicht hebt gemaakt voor de projecten.  
In de foreach loop kun je nu bij elk item een link maken naar deze nieuwe view. Daarbij geef je het project mee aan de route.
Bijvoorbeeld zo in het geval je Model `model` heet:
{% raw %}
```php
        <a href="{{route('model.show', $model)}}">Bekijk dit item</a>
```
{% endraw %}


---
## Testen
Bekijk nu je site en zie dat je van het overzicht naar het project kunt navigeren. 

---

{% include commit_push.md %}

