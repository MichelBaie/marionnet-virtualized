# marionnet-virtualized 🖥️
A Marionnet virtual machine running on Debian 11

## Procédure de construction

1. Partir d’un ISO Debian 11 amd64, compte utilisateur etudiant/etudiant, installer sans environnement de bureau avec serveur SSH et web.

2. Installation d’XFCE4 de manière minimaliste

```bash
apt update
apt install xfce4 xfce4-goodies
```

3. Configuration de l’autologin

```bash
nano /etc/lightdm/lightdm.conf

> autologin-user=etudiant
```

4. Installation des outils additionels pour chaque hyperviseur

```bash
apt install open-vm-tools-desktop qemu-guest-agent hyperv-daemons spice-vdagent
```

5. Installation des outils additionels pour VirtualBox

```bash
apt install build-essentials dkms linux-headers-amd64 --no-install-recommends
bash VBoxLinuxAdditions.run
```

6. Installation des dépendances de Marionnet

```bash
apt install flex bison gawk graphviz uml-utilities bzr opam liblablgtk3-ocaml-dev glade libgtksourceview-3.0-dev libtool bridge-utils gettext fonts-noto elementary-xfce-icon-theme rlfe vde2 libc6-i386 camlp4-extra --no-install-recommends
```

7. Installation de Marionnet

```bash
wget https://bazaar.launchpad.net/~marionnet-drivers/marionnet/trunk/download/head:/useful-scripts/marionnet_from_scratch
bash marionnet_from_scratch
sudo rm -R /root/.opam
```

8. Installation de Konsole

```bash
apt remove xterm
apt install konsole --no-install-recommends
```

9. Activation de Konsole dans la configuration de Marionnet

```
nano /etc/marionnet/marionnet.conf

>MARIONNET_TERMINAL="konsole,-T,-e"
```

10. Installation de Firefox

```
apt install firefox-esr --no-install-recommends
```

11. Ajout du .desktop sur le bureau et personnalisation du lanceur d’applications avec alacarte (catégorie Éducation)

```
apt install alacarte --no-install-recommends
```

12. Désactivation de la mise en veille de l’écran, ainsi que du verouillage automatique

```
Paramètres > Gestionnaire d'alimentation
```

13. Activer Marionnet au démarrage de XFCE (et désactiver Notification Daemon + Verrouilleur d’écran)

```
Paramètres > Session et démarrage
```

14. Modifier GRUB pour que le démarrage se fasse instantanément

```
nano /etc/default/grub

> GRUB_TIMEOUT=0

update-grub
```

15. Définir pour fond d’écran celui de l’Université Sorbonne Paris Nord (ex Univ Paris 13)

```
> graphiquement
```

16. Configurer les permissions sudo de l’utilisateur etudiant

```
nano /etc/sudoers

> etudiant ALL=(ALL) NOPASSWD: ALL
```

16. Redémarrer pour vérifier le bon fonctionnement de la machine virtuelle

```
reboot
```

17. Nettoyer la machine virtuelle

```
apt autoremove
apt autoclean
apt clean
history -c
poweroff
```

18. Démarrer sur la distribution systemrescue pour nettoyer le disque dur de la machine virtuelle

```
zerofree -v /dev/sda1
poweroff
```

19. Configurer les spécifications de la machine à 1 coeur de CPU et 2go de RAM, puis défragmenter et compresser le disque

```
> graphiquement
```

20. Définir la description de la machine

```
Identifiant : etudiant/etudiant
```

21. Convertir le disque en .qcow2

```
qemu-img convert -f vmdk -O qcow2 -c input.vmdk output.qcow2
```

22. Exporter la machine virtuelle via VirtualBox en ova 1.0

```
> graphiquement
```

Zipper et publier !
