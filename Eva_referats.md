title: "Pieteikumu klasifikācija"
author: [Eva Mārtiņsone]
date: "2021-02-22"
subject: "Programmēšana"
keywords: [Markdown, Example]
subtitle: "Referāts"
lang: "en"
titlepage: true,
titlepage-rule-color: "360049"
titlepage-background: "backgrounds/background5.pdf"
...

# 1. Izmantotie moduļi
Izmantots:
pandas.DataFrame modulis izmantots ar mērķi veikt darbības ar datiem tabulā gan pēc rindu, gan pēc kolonnu etiķetēm
smtplib modulis izmatots ar mērķi izsūtīt e-pastu

# 2. CSV faila imports
Izmantotā komanda:
pandas.read_csv - nodrošina csv faila nolasīšanu, kurā ir atdalītas vērtības
r - nodroīna nepabeigtu vērtību tdalīšanu
(faila atrašanās ceļš) - importētā faila atrašanās vieta 

Izpildītais kods:
import pandas as pd
saraksts = pd.read_csv (r'C:\Users\Lietotajs\Desktop\ievades_dati.csv')
print(saraksts)

# 3. CSV faila indeksēšan
Izmantotas komandas:
.index - nodrošina katras tabulas kolonas/līnijas indeksēšanu kā atevišķu vienumu
.loc - nodrošina indeksēto tabulas kolonu/līniju vienumu atlasi

Izpildītais kods
3. 1. Nodrošinas datu indeksēšanu pēc kolonas 'Organizācija'
pak_kolonas = saraksts.set_index('Organizācija')'
print(pak_kolonas)

3. 2. Nodrošina konkrēto vērtību atlasi pēc 1.1. punktā indeksētās kolonas 'Organizācija'
iestade = pak_kolonas.loc[['Labklājības departaments', 'Rīgas Sociālais dienests', 'Rīgas pašvaldības policija', 'Sociālais dienests']]
print(iestade)

3. 3. Nodrošina 3.2. punktā iegūto datu indeksēšanu to tālākai apstrādei pēc kolonas 'Darba grupa'
pak_vaditaji = iestade.set_index('Darba grupai')
print(pak_vaditaj)

3. 4. Nodrošina konkrēto vērtību atlasi pēc 3.3. punktā indeksētajiem datiem, kas nepieciešams e-pastu saturam
Normunds = pak_vaditaji.loc[['Datu bāzu un sistēmu nodaļa']]
print('DBSN pieteikumi', Normunds)

Mihails = pak_vaditaji.loc[['Tehnisko resursu uzturēšanas sektors']]
print('TRU sektota pieteikumi', Mihails)

Jorens = pak_vaditaji.loc[['Fiziskās drošības un integrēto sistēmu sektors']]
print('FDIS sektota pieteikumi', Jorens)

# Epatsu izsūtīšana

import smtplib 

To = "mmmartinsone@gmail.com" 
Subject = "neizpildītie uzdevumi"
Text = 'tetsa e-pasts'

smtp_server = "smtp.gmail.com"
port = 587

#GMail kredinceali
e_pasta_sender = "mmmartinsone@gmail.com"
e_pasta_parole = "parole" 

#pieslegums e-pasta servisiem
server = smtplib.SMTP('smtp.gmail.com', 587)
server.ehlo() 
server.starttls()
server.ehlo() 

server.login(e_pasta_sender, e_pasta_parole)

saturs = '\r\n'.join([
   'To: %s' % To,
   'From: %s' % e_pasta_sender,
   'Subject: %s' % Subject,
   '',
   Text
   ])

try:
   server.sendmail(e_pasta_sender, [To], saturs)
   print('epasts nosūtīts')
except:
   print('e_pasts nav nosūtīts') 
   
server.quit()