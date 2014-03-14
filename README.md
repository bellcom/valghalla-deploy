valghalla-deploy
================
Deployment script for valghalla


Installer Drush og drush make
--------------------
* Udfør: `sudo pear channel-discover pear.drush.org`
* Udfør: `sudo pear install drush/drush`

Hent filer og opret site folder og database m.m.
------------------------------------------
Drupal Version: 7.22

Drush Version: 5.8

Installer Valhalla med drush make filer.

1. `cd [web dir]`
2. `drush dl drupal-7.22 --drupal-project-rename=public_html`
3. `git clone git@github.com:bellcom/valhalla-deploy.git`

    Kør deploy script. Afhængig af hvilken profil der ønskes skal reroll.dev.sh eller reroll.sh køres og linkes til profiles diret. Alle moduler bliver hentet fra master branchen. Hold øje med dette under udvikling. Alle repositories er git repos.

4. `cd valhalla-deploy`, `./reroll.dev.sh` eller `./reroll.sh`. Kan tage lang tid at køre, da den henter alle moduler. Kan kræve sudo. Følg med i log om der sker fejl. Ved fejl på contrib moduler prøv evt igen, da det kan skyldes i dårlig håndtering fra Drush.
5. `cd ../public_html/profiles`
6. `ln -s ../../valhalla-deploy/build/master-latest valhalla` eller `ln -s ../../valhalla-deploy/build/dev-latest valhalla`
7. Udfør `cd ..;cp sites/default/default.settings.php sites/default/settings.php`
8. Udfør `sudo chmod g+rwX /var/www/[dit domæne]`
9. Udfør `sudo chgrp -R www-data /var/www/[dit domæne]`
10. Installer sitet på `http://[dit domæne]/install.php`. Følg guiden, her skal du desuden bruge dine informationer til databasen.
11. Udfør `drush cc registry` og `drush cc all`.
12. Udfør `chmod -w sites/default/settings.php sites/default/`
13. Sæt cron op for sitet. `drush vget cron_key`. Gem key. `sudo crontab -u www-data -e` og indsæt (erstat SITE og KEY): `0 * * * * /usr/bin/wget -O - -q -t 1 'https://SITE/cron.php?cron_key=KEY'`

Proceduren er at reroll.[].sh bruges når moduler skal opdateres fra origin.

Licence and copyright
---------------------
Valghalla is Copyright (c) 2012 OS2 - Offentligt Digitaliseringsfællesskab, Denmark
<http://os2web.dk/>

Valghalla is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

Valghalla is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
ERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
