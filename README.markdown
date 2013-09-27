<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.da"><img alt="Creative Commons licens" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br />Dette værk er licenseret under en <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.da">Creative Commons Navngivelse-DelPåSammeVilkår 3.0 Unported Licens</a>.

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
4. `cd public_html/profiles`

    Kør deploy script. Afhængig af hvilken profil der ønskes skal reroll.dev.sh eller reroll.sh køres og linkes til profiles diret. Alle moduler bliver hentet fra master branchen. Hold øje med dette under udvikling. Alle repositories er git repos.

5. `./reroll.dev.sh` eller `./reroll.sh`. Kan tage meget lang tid at køre, da den henter alle moduler. Kan kræve sudo. Følg med i log om der sker fejl. Ved fejl på contrib moduler prøv evt igen, da det kan skyldes i dårlig håndtering fra Drush. Første gang reroll køres sker der til sidst mange fejl. Dette skyldes den foretager ting på database niveau. Den database vi endnu ikke har oprettet. :-) Dette er OK.
6. `ln -s ../../valhalla-deploy/build/master-latest valhalla` eller `ln -s ../../valhalla-deploy/build/dev-latest valhalla`

7. Udfør `cp sites/default/default.settings.php sites/default/settings.php`
8. Udfør `sudo chmod g+rwX /var/www/[dit domæne]`
9. Udfør `sudo chgrp -R www-data /var/www/[dit domæne]`
10. Installer sitet på `http://[dit domæne]/install.php`. Følg guiden, her skal du desuden bruge dine informationer til databasen.
11. Udfør `drush cc registry` og `drush cc all`.

Proceduren er at reroll.[].sh bruges når moduler skal opdateres fra origin.
