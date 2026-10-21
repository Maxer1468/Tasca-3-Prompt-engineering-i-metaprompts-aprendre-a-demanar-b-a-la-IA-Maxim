# Guia de Seguretat Informàtica, Scripting en Bash i Enginyeria de Prompts (CFGM SMX)

## 1. Pla d'Estudi Express de Seguretat Informàtica (2n CFGM SMX)

Aquest pla està dissenyat per a la comprensió de conceptes clau de seguretat mitjançant analogies i humor.

### Dia 1: La Porta, els Panys i els Permisos

* **Concepte:** Protegir la informació és equivalent a protegir un habitatge o elements personals.

* **Punts clau:**

  * **La Triada CIA:**

    * **Confidencialitat:** La informació només ha de ser accessible per a usuaris autoritzats.

    * **Integritat:** Les dades no s'han de modificar sense permís.

    * **Disponibilitat:** La informació ha d'estar accessible quan es requereixi.

    * *Analogia/Broma:* Com l'historial de cerca de Google: ha de ser confidencial, ningú l'ha de modificar i ha d'estar disponible quan es busca un mem antic.

  * **Protecció física i SAI/UPS:** Servidors sota clau i ús de sistemes d'alimentació ininterrompuda per evitar caigudes per Talls elèctrics.

    * *Analogia/Broma:* Un SAI evita que el servidor es quedi "grogui" i caigui rodó a mitja feina.

  * **Permisos d'accés (Mínim Privilegi):** Cada usuari disposa únicament dels accessos estrictament necessaris per a la seva funció.

    * *Analogia/Broma:* No es lliura la clau de casa ni el PIN de la targeta al repartidor; tampoc s'ha de concedir permís de `root` a qualsevol programa.

### Dia 2: El Segurata, les Vacunes i les Contrasenyes

* **Concepte:** Prevenció d'intrusions i programari maliciós.

* **Punts clau:**

  * **Contrasenyes i Doble Verificació (MFA):** Llargada de claus i codi addicional de confirmació.

    * *Analogia/Broma:* Utilitzar `123456` o `admin` és una invitació formal a la teva vida digital.

  * **El Tallafocs (Firewall):** Filtre de tràfic d'entrada i sortida de la xarxa.

    * *Analogia/Broma:* El segurata de discoteca que bloqueja l'accés en xandall, però aplicat a ports de xarxa.

  * **Antivirus i Actualitzacions:** Manteniment de defenses davant noves amenaces.

    * *Analogia/Broma:* Ignorar el missatge de "Nova actualització disponible" durant 6 mesos és com veure ploure, obrir la finestra i pensar que no et mollaràs.

### Dia 3: Assegurar-se contra Incendis (Còpies de Seguretat)

* **Concepte:** Resguard de dades davant fallades del sistema.

* **Punts clau:**

  * **La regla 3-2-1:** 3 còpies de seguretat, en 2 suports diferents, i 1 còpia fora de la localització principal (ex: núvol).

    * *Analogia/Broma:* Tenir només una còpia al mateix ordinador és jugar a la ruleta russa amb el disc dur (el disc dur sempre guanya).

  * **Prova de restauració:** Comprovar periòdicament que els backups es poden restaurar.

    * *Analogia/Broma:* Fer còpies i no provar-les és com comprar un paracaigudes de segona mà i no obrir-lo fins al moment del salt.

## 2. Avaluació de Fets Verificables vs. Estimacions Pedagògiques

Classificació dels elements del pla d'estudi segons la seva naturalesa tècnica o de planificació.

| Afirmació / Concepte | Categoria | Nivell de Confiança | Justificació / Verificació | 
| ----- | ----- | ----- | ----- | 
| **Triada CIA** | Fet Verificable | **100% (Molt Alt)** | Model de seguretat reconegut per l'estàndard **ISO/IEC 27001**. | 
| **Principi de Mínim Privilegi (UGO / ACLs)** | Fet Verificable | **100% (Molt Alt)** | Concepte fonamental en administració de sistemes POSIX (Linux) i NTFS (Windows). | 
| **Execució com a `root`** | Fet Verificable | **100% (Molt Alt)** | Comportament del nucli Linux: l'UID 0 no té restriccions d'accés estàndard. | 
| **Regla 3-2-1 de Backup** | Fet Verificable | **95% (Molt Alt)** | Bones pràctiques recomanades per organitzacions com la CISA o l'INCIBE. | 
| **Ports i Tallafocs** | Fet Verificable | **100% (Molt Alt)** | Assignació oficial de ports per l'**IANA** (ex: SSH 22, HTTP 80, HTTPS 443). | 
| **SAI/UPS per a talls elèctrics** | Fet Verificable | **100% (Molt Alt)** | Propietat física i elèctrica del maquinari de suport. | 
| **Completar el pla en 3 dies (45-60 min/dia)** | Estimació / Predicció | N/A | Depèn del ritme d'aprenentatge i background de l'estudiant. | 
| **Organització del pla en 3 blocs** | Opinió Metodològica | N/A | Estructura pedagògica basada en el currículum de 2n d'SMX. | 
| **Utilitat de les analogies** | Opinió Pedagògica | N/A | L'eficàcia d'una analogia depèn de la percepció individual. | 

## 3. Automatització en Linux: Script de Còpia de Seguretat (`backup_simple.sh`)

Script de Bash desenvolupat per a entorns Ubuntu Server per automatitzar backups.

```
#!/bin/bash

# 1. Definim les rutes d'origen i destinació
ORIGEN="/var/www/html"
DESTINACIO="/var/backups/meus_backups"

# 2. Generem la marca de temps actual (Any-Mes-Dia_Hora-Minut)
DATA=$(date +%Y-%m-%d_%H-%M)

# 3. Comprovem si el directori d'origen existeix
if [ ! -d "$ORIGEN" ]; then
    echo "Error: El directori d'origen $ORIGEN no existeix."
    exit 1
fi

# 4. Creem el directori de destinació si encara no existeix
mkdir -p "$DESTINACIO"

# 5. Creem el fitxer .tar.gz comprimit
tar -czf "$DESTINACIO/backup_$DATA.tar.gz" "$ORIGEN"

# 6. Missatge de confirmació
echo "Còpia de seguretat creada amb èxit a: $DESTINACIO/backup_$DATA.tar.gz"

```

### Instruccions d'execució i assignació de permisos:

```
# Donar permisos d'execució a l'usuari propietari
chmod +x backup_simple.sh

# Executar l'script
./backup_simple.sh

```

## 4. Enginyeria de Prompts: Metodologia i Plantilles

### 4.1. Estructura Bàsica d'un Prompt Tècnic

* **\[Rol\]:** Defineix la perspectiva i el tom de la IA.

* **\[Context\]:** Fixa l'entorn de treball i els antecedents.

* **\[Tasca\]:** Descriu l'objectiu concret a executar.

* **\[Públic\]:** Determina el nivell de complexitat i explicació requerit.

* **\[Format\]:** Defineix l'estructura visual del resultat (codi, taules, text).

* **\[Restriccions\]:** Delimita les eines permeses, sintaxi i exclusions.

### 4.2. Avaluació d'un Prompt Ambigu vs. Versió Millorada

* **Prompt Original:** `fes-me un resum sobre Seguretat informatica`

* **Puntuació Global:** 2/10.

#### Anàlisi de Dificultats:

1. **Claredat (4/10):** Absència de definició de l'abast del resum.

2. **Context (0/10):** No especifica el nivell acadèmic ni l'objectiu.

3. **Especificitat de la tasca (2/10):** No delimita els temes de seguretat a tractar.

4. **Format (1/10):** Manquen indicacions sobre l'organització de la informació.

5. **Restriccions (1/10):** Absència de límits de longitud o terminologia.

#### Versió Optimitza del Prompt:

> **\[Rol\]:** Actua com un professor de cicle formatiu d'informàtica.
>
> **\[Context\]:** Soc estudiant de 2n de CFGM d'SMX i estic preparant un esquema de repàs ràpid per a l'examen del mòdul de Seguretat Informàtica.
>
> **\[Tasca\]:** Fes un resum dels 5 blocs fonamentals de l'assignatura: Triada CIA, seguretat física/SAI, permisos de sistema (UGO/ACLs), protecció activa (tallafocs/antivirus) i còpies de seguretat (regla 3-2-1).
>
> **\[Públic\]:** Estudiant de nivell tècnic mitjà.
>
> **\[Format\]:** Utilitza una taula Markdown amb 3 columnes: `Concepte | Explicació en una frase | Error típic a evitar`.
>
> **\[Restriccions\]:** Utilitza un llenguatge pràctic i directe, evita tecnicismes excessivament teòrics o avançats i no superis les 300 paraules en total.

### 4.3. Procés de Disseny d'un Prompt Reutilitzable per a Backup

Pas a pas de les especificacions requerides per a la creació de l'script de backup:

1. **Objectiu:** Script d'automatització en Bash per a entorns Linux.

2. **Lògica d'Execució:**

   * Definició de rutes i variables.

   * Validació d'existència de l'origen (`if [ -d ... ]`) i sortida (`exit 1`).

   * Creació de la destinació amb `mkdir -p`.

   * Generació de timestamp (`date +%Y%m%d_%H%M%S`).

   * Empaquetatge i compressió amb `tar -czf`.

   * Comprovació del codi de retorn (`$?`) i confirmació per terminal.

3. **Format Requerit:**

   * Bloc de codi Markdown (`bash`).

   * Comentaris línia per línia en català o castellà.

   * Sense complexitat innecessària (Nivell SMX).

   * Instruccions d'execució (`chmod +x` i `./script.sh`).

4. **Restriccions:** Comandes estàndard POSIX/Linux, aplicable a 2n d'SMX.

### 4.4. Col·lecció de Prompts Tècnics Reutilitzables (Format RCTFPR)

#### Prompt 1: SystemPrompt Architect (Metaprompt)

* **Finalitat:** Generar prompts d'alta precisió per a qualsevol àmbit informàtic.

```
[Rol]: Ets un enginyer de Prompt Engineering especialitzat en infraestructures TIC, administració de sistemes i desenvolupament de programari.
[Context]: L'usuari necessita dur a terme una tasca tècnica complexa d'informàtica: [OBJECTIU_O_TASCA_TECNICA], però necessita un prompt d'IA optimitzat per obtenir la millor resposta possible en futures consultes.
[Tasca]: Redacta un prompt final perfectament estructurat utilitzant la metodologia RCTFPR (Rol, Context, Tasca, Format, Paràmetres, Restriccions) que l'usuari pugui copiar i utilitzar directament.
[Format]: Presenta la resposta amb les seccions del prompt clarament delimitades i inclou entre claudàtors les variables que l'usuari haurà d'emplenar en utilitzar-lo.
[Paràmetres]: Assegura't que el prompt generat obligui la IA a ser extremadament rigorosa amb la sintaxi, la seguretat i les bones pràctiques del sector informàtic.
[Restriccions]: No resolguis la tasca tècnica en si mateixa; limita't a construir el prompt optimitzat.

```

* **Variables a canviar:** `[OBJECTIU_O_TASCA_TECNICA]`

* **Criteri de verificació:** Generació d'un prompt estructurat RCTFPR directament utilitzable en altres models d'IA amb respostes sense ambigüitats.

#### Prompt 2: BashScript Pro

* **Finalitat:** Automatització i auditoria de la creació d'scripts en Bash per a administració de sistemes Linux.

```
[Rol]: Ets un administrador de sistemes Linux sènior i expert en seguretat de Bash.
[Context]: Necessito automatitzar una tasca repetitiva al servidor per estalviar temps i minimitzar errors humans.
[Tasca]: Genera un script de Bash robust i net que faci exactament el següent: [DESCRIPCIÓ_DE_LA_TASCA]. Inclou control d'errors (com comprovació de codis de sortida o set -e) i comentaris detallats pas a pas.
[Format]: Codi en bloc Markdown net, seguit d'una breu explicació de com executar-lo i quins permisos necessita.
[Paràmetres]: El codi ha de ser compatible amb distribucions basades en Debian/Ubuntu, utilitzar variables clares i gestionar correctament els permisos UGO si s'escau.
[Restriccions]: No incloguis ordres destructives (com rm -rf o modificacions massives de fitxers de sistema) sense una validació prèvia o avís clar a l'usuari.

```

* **Variables a canviar:** `[DESCRIPCIÓ_DE_LA_TASCA]`

* **Criteri de verificació:** Validació de sintaxi sense errors (`bash -n`) i execució autònoma amb missatges d'estat clars.

#### Prompt 3: DockerCompose Architect

* **Finalitat:** Disseny de fitxers `docker-compose.yml` optimitzats i entorns multi-contenidor.

```
[Rol]: Ets un arquitecte de programari i expert en containerització amb Docker i Docker Compose.
[Context]: Necessito desplegar un entorn multi-contenidor de manera neta, aïllada i reproducible per a [PROJECTE_O_APLICACIO].
[Tasca]: Construeix un fitxer docker-compose.yml complet que inclogui els serveis necessaris, volums persistents per a les dades, xarxes internes de servei i variables d'entorn segures.
[Format]: Mostra el fitxer de configuració en un bloc de codi YAML i acompanya'l d'un fitxer .env.example necessari i de les instruccions exactes per engegar-ho.
[Paràmetres]: Utilitza versions estables d'imatges oficials de Docker Hub i bones pràctiques de gestió de ports i persistència.
[Restriccions]: El fitxer ha de ser directament funcional i no requerir modificacions complexes addicionals de sintaxi.

```

* **Variables a canviar:** `[PROJECTE_O_APLICACIO]`

* **Criteri de verificació:** Desplegament del comando sense conflictes de ports o imatges, deixant els contenidors en estat `running`.

## Link conversa IA: https://share.gemini.google/9UUq6ac1UTIy