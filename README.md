# Practica de Git, GitHub y SourceTree
----------

- **¿Qué comando utilizaste en el paso 11? ¿Por qué?**
	
```
git reset --hard HEAD~1
```
Empleo este comando por que es el único que permite mover el puntero de la rama donde estoy al punto donde quiera. Empleando el atriburo *--hard* me permite modificar el *working copy*. **HEAD~1** me permite restar un commit a la posición **HEAD**. En resumen este comando me permite mover el puntero **HEAD** y el puntero de la rama a una posicion predeterminada en este caso la posición del **HEAD-1**. 

- **¿Qué comando o comandos utilizaste en el paso 12? ¿Por qué?**
	
Para poder recuperar los cambios que hemos deshecho. Es necesario recuperar el hash del ultimo commit. Cada commit tiene un hash SHA1 que lo identifica de forma única. Para ello primeramente he empleado el comando:
	
	```
	git reflog
	```
Mediante este comando vemos todas las acciones que se hemos realizado sobre nuestro repositorio local, para recuperar el ultimo commit. 
	> acfa857 HEAD@{0}: reset: moving to acfa857
	
	> 2b3e197 HEAD@{1}: reset: moving to HEAD~1
	
	> acfa857 HEAD@{2}: commit: Modified git nuestro
	
	> 2b3e197 HEAD@{3}: checkout: moving from master to 	styled
	
	> 2b3e197 HEAD@{4}: commit (initial): Added Git Nuestro
	
	Podemos ver que el hemos realizado sobre el repositorio. Podemos ver el hash (corto) del commit de haber modificado el poem.md y cambiado el color por las etiquetas *HTML*. 
	
	```
	git reset --hard acfa857
	```
	El comando reset aparte de admitir posiciones sobre **HEAD** también admite hash.

- **El merge del paso 13, ¿Causó algún conflicto? ¿Por qué?**

No causa ningún conflicto al realizar el comando:
```
git merge master 
```
El porque no causa ningún error es que no se puede hacer un merge de **styled** a **master** ya que **styled** ya contiene lo que tiene **master** por eso el mensaje que sale es:
	```
	> Already up-to-date.
	```
**style** esta más avanzada y contiene los *Hunks* de la rama **master**

- **El merge del paso 19, ¿Causó algún conflicto? ¿Por qué?**

Al ejecutar el paso 19, el cual se resuelve con el comando:
	
	```
	git merge htmlify
	```
	
Si generan conflictos, aunque git es bastante inteligente a la hora de crear y eliminar filas, no es capaz de hacerlo cuando se modifican en las dos ramas las mismas líneas, por esa razón debemos modificar los conflictos a mano. En este estado Git se queda realizando el merge a la espera que hagamos un commit con los cambios resueltos. Por lo que se procede con **nano** a modificar y realizar el commit

- **El merge del paso 21, ¿Causó algún conflicto? ¿Por qué?**

Al ejecutar el comando

```	
git merge htmlify
```

No causa ningún conflicto ya que el merge que esta realizando es un *fast forward* quiere decir que el grafo de git se puede simplificar en una lista, por lo tanto para realizar el *merge* lo único que debemos hacer es mover la *branch* de master a styled, quedando master y styled en el mismo *commit* (Únicamente mueve el puntero de la rama a la nueva posición)

- **¿Qué comando o comandos utilizaste en el paso 25?**

Primeramente he añadido un alias, dicho alias me permite un comando de git ejecutar un comando mas complejo, para añadir un alias debemos realizar el siguiente comando:

```
git config alias.graph "log --graph --decorate --pretty=oneline"
```
	
La descripción del contenido del git que se añade a la configuración un nuevo alias, que es nombrado **graph** y que es el comando git **log --graph --decorate --pretty=oneline** 

Una vez que hemos ejecutado el comando debemos ejecutar el comando: 
	
```
git graph
```
	
Para que nos aparezca la otra información. 	
El diagrama que he salido por pantalla es el siguiente:
<pre>
	*   0aa310ad465bd2ec56f5dd340d7d1e8cf21662c2 (HEAD -> master, styled) Merged
	|\
	| * 2e974407d4f1d86836ffc7d1182d08a6e0530008 (htmlify) Add new git 	nuestro
	* | acfa857bda7d3b12263563b3eb9bdcc6a5f49c5b Modified git nuestro
	|/
	* 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc Added Git Nuestro
</pre>

		

- **El merge del paso 26, ¿Podría ser fast forward? ¿Por qué?**

Si podría ser *fast forward*, la razón de ello es que se pueden traducir el grafo de git como una lista. Solo añadiendo los *hunks* del title quedaria modificado el head. (Ya que la rama title, sale de la rama master)
	
<pre>
	*   f2080fa47f4772bfe9d48842cfefc8d201f1e911 (HEAD -> master) Merge 	branch 'title' no fast forward
	|\
	| * c4350f9948f2d3b908d1ebd711a2f67eb49b206d (title) Added Correct 	title
	|/
	*   0aa310ad465bd2ec56f5dd340d7d1e8cf21662c2 (styled) Merged
	|\
	| * 2e974407d4f1d86836ffc7d1182d08a6e0530008 (htmlify) Add new git 	nuestro
	* | acfa857bda7d3b12263563b3eb9bdcc6a5f49c5b Modified git nuestro
	|/
	* 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc Added Git Nuestro
</pre>
	
Podemos ver que realizando el comando
	
```
git merge title --no-ff
```
	
Si hubiesemos ejecutado fast forward quedaría asi: 
	
<pre>
	*   f2080fa47f4772bfe9d48842cfefc8d201f1e911 (HEAD -> master) Merge 	branch 'title' fast forward
	|
	*   0aa310ad465bd2ec56f5dd340d7d1e8cf21662c2 (styled) Merged
	|\
	| * 2e974407d4f1d86836ffc7d1182d08a6e0530008 (htmlify) Add new git 	nuestro
	* | acfa857bda7d3b12263563b3eb9bdcc6a5f49c5b Modified git nuestro
	|/
	* 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc Added Git Nuestro
</pre>


	
- **¿Qué comando o comandos utilizaste en el paso 27?**

Para deshacer el merge tenemos que realizar un *git reset* exactamente:
	
```
git reset HEAD~1
```
	
En este paso debemos obviar el parámetro *--hard* por que queremos mantener el los cambios del *working copy*. El comando es *HEAD~1* por que sin nos fijamos en el grafo debemos reducir el paso anterior
	
Como seguimos en la rama **master**, no podemos ver la rama **title** por esa razón el grafo queda de la forma de arriba.
	
- **¿Qué comando o comandos utilizaste en el paso 28?**

	Para descartar los cambios podemos realizar dos formas diferentes:
	
	1. Podemos realizar un *reset* de la rama actual con el parametro *--hard*. 
		
		```
		git reset --hard HEAD
		```
		Este comando restaurara todos los ficheros y dejara el *working copy* como estuviera en el repositorio.
		
	2. Podemos realizar un *checkout* de cada archivo que queramos para poder descartar los cambios.  
		
		```
		git checkout -- git-nuestro.md
		```		
		Este comando permite devolver cada uno de los archivos de forma independiente el estado en el cual estuviera en el repositorio. 

- **¿Qué comando o comandos utilizaste en el paso 29?**

	El comando para eliminar la rama es el siguiente:
	
	```
	git branch -D title
	```
	
	Dicho comando borra la rama, pero no es un borrado normal sino un borrado forzoso ya que si se realiza este comando con el parámetro *-d* no borrara la rama por que no esta mergueada y podríamos perder datos.

- **¿Qué comando o comandos utilizaste en el paso 30?**

Primeramente necesitamos realizar un comando para ver que hemos hecho sobre el repositorio. Para ello debemos ejecutar el comando:
	
	```
	git reflog
	```
Este comando permite mirar las acciones realizadas sobre el repositorio:
	
<pre>
	0aa310a HEAD@{0}: reset: moving to HEAD~1
	f2080fa HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
	0aa310a HEAD@{2}: checkout: moving from title to master
	c4350f9 HEAD@{3}: commit: Added Correct title
	0aa310a HEAD@{4}: checkout: moving from master to title
	0aa310a HEAD@{5}: merge styled: Fast-forward
	2b3e197 HEAD@{6}: checkout: moving from styled to master
	0aa310a HEAD@{7}: commit (merge): Merged
	acfa857 HEAD@{8}: checkout: moving from master to styled
	2b3e197 HEAD@{9}: checkout: moving from htmlify to master
	2e97440 HEAD@{10}: commit: Add new git nuestro
	2b3e197 HEAD@{11}: checkout: moving from master to htmlify
	2b3e197 HEAD@{12}: reset: moving to 2b3e197
	0392034 HEAD@{13}: commit: htmlify
	2b3e197 HEAD@{14}: checkout: moving from styled to master
	acfa857 HEAD@{15}: reset: moving to acfa857
	2b3e197 HEAD@{16}: reset: moving to HEAD~1
	acfa857 HEAD@{17}: commit: Modified git nuestro
	2b3e197 HEAD@{18}: checkout: moving from master to styled
	2b3e197 HEAD@{19}: commit (initial): Added Git Nuestro
</pre>
	
Estas son las acciones realizadas sobre el repositorio, como podemos ver las acciones interesantes para recuperar el *merge* del title es el siguiente:
	
	> f2080fa HEAD@{1}: merge title: Merge made by the 'recursive' strategy.
	
Si después ejecutamos el comando *reset* y movernos a dicho commit.
	
	```
	git reset --hard HEAD@{1}
	```  
Una vez realizado el comando podemos ver como en el grafo se muestra el estado anterior sin mantener la branch **title**:
	
<pre>
	*   f2080fa47f4772bfe9d48842cfefc8d201f1e911 (HEAD -> master) Merge 	branch 'title' no fast forward
	|\
	| * c4350f9948f2d3b908d1ebd711a2f67eb49b206d Added Correct title
	|/
	*   0aa310ad465bd2ec56f5dd340d7d1e8cf21662c2 (styled) Merged
	|\
	| * 2e974407d4f1d86836ffc7d1182d08a6e0530008 (htmlify) Add new git nuestro
	* | acfa857bda7d3b12263563b3eb9bdcc6a5f49c5b Modified git nuestro
	|/
	* 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc Added Git Nuestro
</pre>
	
- **¿Qué comando o comandos usaste en el paso 32?**

Para volver al commit inicial debemos realizar un *reset* y movernos a la primera posición para ello debemos ejecutar el comando:
	
	```
	git log
	```
	
Con el resultado del comando es el siguiente:
	
<pre>
		commit f2080fa47f4772bfe9d48842cfefc8d201f1e911
	Merge: 0aa310a c4350f9
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 14:07:13 2016 +0200
	
	    Merge branch 'title' no fast forward
	
	commit c4350f9948f2d3b908d1ebd711a2f67eb49b206d
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 14:01:41 2016 +0200
	
	    Added Correct title
	
	commit 0aa310ad465bd2ec56f5dd340d7d1e8cf21662c2
	Merge: acfa857 2e97440
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 13:54:49 2016 +0200
	
	    Merged
	
	commit 2e974407d4f1d86836ffc7d1182d08a6e0530008
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 13:30:31 2016 +0200
	
	    Add new git nuestro
	
	commit acfa857bda7d3b12263563b3eb9bdcc6a5f49c5b
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 12:11:29 2016 +0200
	
	    Modified git nuestro
	
	commit 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc
	Author: wholedev <a.whole.dev@gmail.com>
	Date:   Sun Jun 19 12:09:03 2016 +0200
	
	    Added Git Nuestro
</pre>

Si queremos volver al primer estado deberemos realizar el comando *reset* con el parametro *--hard*

```
git reset --hard 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc
```
	
Mediante el comando que hemos realizado ya nos permite estar en la posición deseada, como se muestra en el grafo a continuación:
	
<pre>
	* 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc (HEAD -> master) Added Git Nuestro
</pre>


- **¿Qué comando o comandos usaste en el punto 33?**

Primeramente debemos conocer los hash, primeramente debemos el log. Para ello empleamos el comando: 
	
	```
	git reflog
	```
Los datos que me aparecen los siguientes:
	
```
2b3e197 HEAD@{0}: reset: moving to 2b3e197ef2b458ec7ffec21fe49f5e766fae62dc
f2080fa HEAD@{1}: reset: moving to HEAD@{1}
0aa310a HEAD@{2}: reset: moving to HEAD~1
f2080fa HEAD@{3}: merge title: Merge made by the 'recursive' strategy.
0aa310a HEAD@{4}: checkout: moving from title to master
c4350f9 HEAD@{5}: commit: Added Correct title
0aa310a HEAD@{6}: checkout: moving from master to title
0aa310a HEAD@{7}: merge styled: Fast-forward
2b3e197 HEAD@{8}: checkout: moving from styled to master
0aa310a HEAD@{9}: commit (merge): Merged
acfa857 HEAD@{10}: checkout: moving from master to styled
2b3e197 HEAD@{11}: checkout: moving from htmlify to master
2e97440 HEAD@{12}: commit: Add new git nuestro
2b3e197 HEAD@{13}: checkout: moving from master to htmlify
2b3e197 HEAD@{14}: reset: moving to 2b3e197
0392034 HEAD@{15}: commit: htmlify
2b3e197 HEAD@{16}: checkout: moving from styled to master
acfa857 HEAD@{17}: reset: moving to acfa857
2b3e197 HEAD@{18}: reset: moving to HEAD~1
acfa857 HEAD@{19}: commit: Modified git nuestro
2b3e197 HEAD@{20}: checkout: moving from master to styled
2b3e197 HEAD@{21}: commit (initial): Added Git Nuestro
```
	
Una vez realizado debemos emplear lógica para descubrir en que acción debemos recuperar, si miramos el log podemos ver que nos hemos movido cuando hemos empleado el merge era el hash **f2080fa**, por esa razón una vez realizado el *reset* a dicha posición tendremos el estado anterior: 
	
```
	git reset --hard f2080fa
```
	
Debemos añadir el comando *--hard* ya que se debe actualizar el *working directory*.
	