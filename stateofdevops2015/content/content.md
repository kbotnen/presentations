#### Hva ønsker vi å oppnå

- Kontinuerlig forbedring
- Kontinuerlig levering
- Stabilt driftsmiljø
- Samarbeid mellom seksjoner og grupper
- Mindre personavhengighet
- Økt gjennomsiktighet



#### Hvordan ønsker vi å oppnå målene nevnt over?



### En felles verktøykasse



- Git (versjonshåndtering)
- Puppet (konfigurasjonsmanagement)
- Ansible (orkestrering)
- Jenkins (kontinuerlig integrasjon)
- Python, Php, Ruby, Bash (programmeringsspråk)
- Vagrant, Virtualbox, Vmware, Openstack, libvirt (virtualisering)
- Logstash (logging)



### Jobbe smartere



#### Egne miljøer for utvikling, test og produksjon

- Gjør det enklere å styre endringer
- ITIL (Endringsprosessen)
- Mer stabilt driftsmiljø
- På klienter og servere, i pakker og applikasjoner



#### Infrastruktur som kode

- Programmatisk definerte tilstander på systemer
- Koden dokumenterer systemet; systemdokumentasjonen er dynamisk
- Enklelt å implementere miljøer for utvikling, test og produksjon
- Konfigurasjonsdata er versjonerbare



- Unngår manuelle feil
- Unngår avvik mellom konfigurasjon og dokumentasjon
- Unngår konfigurasjonsdrift
- Gjør det lettere å rulle tilbake endringer
- Ekstremt tidsbesparende!



#### Deling av informasjon

- Infrastruktur som kode i Git gir økt gjennomsiktighet
- Dokumentere oppsett, fremgangsmåter med mer, slik at flere kan
lære mer
- Mindre personavhengighet



### Hva har vi gjort til nå?



- Vi har ikke hatt et styrt DevOps løp
- Vokst seg gradvis frem
- Endret  måten vi jobber på
- Endret verktøyene vi bruker
- Ikke kommet ovenfra og ned
- Behov for å være smartere når det gjelder versjonskontroll, serverkonfig,
orkestrering, deling av informasjon med mer



### Historietime



#### Versjonshåndtering

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_versjonshaendtering.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553e947b-1558-453e-8826-0b310a00c609/image.png)-->


#### Versjonshåndtering

- Startet i IA gruppen
- CVS på MiSide i 2006
- Konfigurasjonsendring i henhold til .backup / .old regime
- Versjonshåndtering via "TSM"
- Gisle presenterte Git rett etter at han begynte på avdelingen
- Egen intern gitolite server git.uib.no i 200X
- Git workshop i 2009 på IA gruppen



#### Konfigurasjonsmanagement med Puppet

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_konfigurasjonsmanagement.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553ea0dc-5ae4-4554-adb5-18a80a004a17/image.png)-->


#### Konfigurasjonsmanagement med Puppet

- Klientdrift har fungert som en sandkasse for utprøving av konsepter fra ca. 2012
- Siden 2014 har alle nye servere blitt satt opp med Puppet
- RHEL 7 blir brekkstang for å komme videre


#### Orkestrering

- Tradisjonelt vært smarte bash script liggende på en eller annen sin maskin
- I 2013 testet vi Mcollective kombinert med dokumentasjon av bruk på itwiki
- I 2015 gikk vi over til Ansible med playbooks i Git og dokmentasjon på itwiki


#### Kontinuerlig integrasjon

![Image Alt](https://www.lucidchart.com/publicSegments/view/553ea9e9-4ae8-4648-a641-05340a009639/image.png)


#### Kontuerlig integrasjon
- Unittesting via Jenkins
- Drar ned kode fra Git til test
- Har testet Selenium, men ikke i aktiv bruk nå



### Deling av informasjon

![Image Alt](http://folk.uib.no/kbo041/devops/images/timeline_delingavinformasjon.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/553eb0ab-0bf4-4f04-a9ad-64330a005c11/image.png)-->


#### Deling av informasjon

- Dokumentasjon har gått fra worddokumenter på p: til mediawiki
- Mediawiki har historikk og er mer tilgjengelig en filer på disk
- Workshop mellom drift og utvikling gir innblikk i hvordan ting gjøres hos andre
og hvilke utfordringer de forskjellige gruppene har, månedlig fra høsten 2014



### Utfordringer?



### Kultur og endring av kultur!



- Krever at en bryr seg om helheten, det vil si at en må ha en holistisk tilnærming til utvikling og infrastruktur!
- Krever en teamtankegang for å lykkes
- Krever at en jobber og forstår på tvers av etablerte faggrupper
- Endring av hvordan folk arbeider



## Empati



- Mellom utviklere og driftere
- Med de som konsumerer tjenestene



#### Devops i praksis



#### Eksempel: Utrulling av en applikasjon

- Provisjoner en ny server med Puppet
- RHEL-base med appstack
- Selve applikasjonen




#### Provisjonering av server

![Image Alt](http://folk.uib.no/kbo041/devops/images/provisjonering_av_server.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/55395b6c-2f2c-40a9-88d8-6c960a00d7d7/image.png)-->


Konfigurasjon av server
```
# Class: platform::el7
#
# This is the common UiB server setup for the Enterprise Linux 7 (el7) platform
#
# == Actions
#
# Install and configure the el7 system
#
#
# == Examples
#
#   class { platform::el7: }
#
#
# == Authors
# Raymond Kristiansen <raymond@uib.no>
#
class platform::el7() {

  $use_fail2ban = hiera('use_fail2ban', true)
  $use_firewall = hiera('use_firewall', true)
  $serverauth   = hiera('serverauth', 'sssd')

  # Verifying class parameters with validate_re from stdlib
  validate_re($platform, hiera('platforms'))
  validate_re($role, hiera('roles'))
  validate_re($data_env, hiera('data_envs'))

  # Unless we are a puppetmaster we should add the puppet module
  unless hiera('puppetmaster') {
    $puppet_env = hiera_hash('puppet_env')
    $env = $::environment? { /rts([0-9]*)/ => 'dev', default => $::environment }

    class { '::puppet':
      pluginsync        => $puppet_env[$env]['puppet_pluginsync'],
      report            => $puppet_env[$env]['puppet_report'],
      server            => $puppet_env[$env]['puppet_server'],
      ca_server         => $puppet_env[$env]['puppet_ca_server'],
      environment       => $::environment,
      masterport        => $puppet_env[$env]['puppet_masterport'],
      usecacheonfailure => $puppet_env[$env]['puppet_usecacheonfailure'],
      mode              => $puppet_env[$env]['puppet_mode'],
      tag               => 'bootstrap',
      packages          => '',
    }
  }

  # Packages
  $packages = hiera_hash('packages', {})
  create_resources ('package', $packages)

  # Remove bootstrap package
  package {'uib-puppet-bootstrap':
    ensure    => absent,
    tag       => 'bootstrap'
  }

  # RHN register
  class { '::rhn_register': tag => 'bootstrap' }
  $rhn_repos = hiera_hash('rhn_register::repos', {} )
  create_resources ('rhn_register::repo', $rhn_repos, { tag => 'bootstrap' })

  # Set up yum repos
  class { '::yum': purge_yumreposd => false }
  class { '::yum::repo::epel': tag => 'bootstrap' }
  $yum_repos = hiera_hash('yum_repos')
  create_resources ('yum::repo', $yum_repos, { tag => 'bootstrap' } )
  class { '::yum::cron': } # Use yum-cron

  # Add sudoers module
  class { '::sudoers':
    timeout_value     => hiera('sudoers_timeout'),
    purge_sudoersd    => hiera('sudoers_purge_sudoersd'),
    keep_git_env      => hiera('sudoers_keep_git_env'),
    keep_ssh_env      => hiera('sudoers_keep_ssh_env'),
    tag               => 'bootstrap',
  }

  # Add users and groups to sudoers
  $sudoers = hiera_hash('sudoers')
  create_resources ('sudoers::add', $sudoers, {
    require => Class['::sudoers'],
    tag => 'bootstrap',
   } )

  # Set up krb5 on bootstrap
  $keytabs = hiera_hash('keytabs', undef)
  class { '::krb5':
    keytabs => $keytabs,
    tag => 'bootstrap'
  }

  # serverauth should be either sssd or ldap
  if $serverauth == "sssd" {
    class { '::authconfig':
      sssd => true,
      krb  => false,
      ldap => false,
      require => Class["::sssd"]
    }
    class { '::sssd':
      override_homedir => hiera('sssd_override_homedir'),
      ldap_uri         => hiera('ldap_uri'),
      tag              => 'bootstrap',
    }
  }
  elsif $serverauth == "ldap" {
    class { '::authconfig':
      sssd => false,
      krb  => true,
      ldap => true,
      require => Package["nss-pam-ldapd"]
    }
    package{"nss-pam-ldapd":
      ensure => installed,
    }
    package{["ipa-client", "sssd","sssd-client","libsss_idmap"]:
      ensure => absent,
    }
  }

  # Add users with pam_access, will not be enabled unless authconfig::pam_access = true.
  class { '::pam_access':
    access_list => hiera_hash("useraccess")
  }

  # Set up firewall
  if $use_firewall {
    Firewall {
      before  => Class['::uib_fw::post'],
      require => Class['::uib_fw::pre'],
    }

    # Purge firewall chain, but ignore fail2ban rules if used
    firewallchain { 'INPUT:filter:IPv4':
      purge  => true,
      ignore => $use_fail2ban? {
        true => ['-p tcp -m tcp --dport 22 -j f2b-SSH'],
        default => undef
      },
      before => Class['::firewall'],
    }
    firewallchain { 'FORWARD:filter:IPv4':
      purge  => true,
      before => Class['::firewall'],
    }
    firewallchain { 'POSTROUTING:nat:IPv4':
      purge  => true,
      before => Class['::firewall'],
    }

    class { '::uib_fw::pre': tag => 'bootstrap' }
    class { '::uib_fw::post': tag => 'bootstrap' }
    class { '::firewall': tag => 'bootstrap' }

    # Apply all firewall rules here
    $firewall_rules = hiera_hash('firewall_rules', {})
    create_resources ('uib_fw::rules', $firewall_rules)

  }

  # fail2ban with jails
  if $use_fail2ban == true {
    class { '::fail2ban': }
    $jails = hiera_hash('fail2ban_jails', {})
    create_resources ('fail2ban::jail', $jails, { require => Class['::fail2ban'] })
  }

  # Set up SSH
  class { '::ssh': }
  $sshd_rules = hiera_hash('sshd', {})
  create_resources('ssh::config::sshd', $sshd_rules)

  # Logrotate rules
  $logrotate_rules = hiera_hash('logrotate_rules', {})
  create_resources('logrotate::rule', $logrotate_rules)

}
```


Konfigurasjon av webserver
```
# == Class: httpd
#
# This sets up a simple Apache HTTPD server
#
# === Parameters
#
# [*replace*]
#   If this is set to true we replace all config files with puppet,
#   otherwise we just insure the file is in place
#
# [*config_dir*]
#   Explanation of what this parameter affects and what it defaults to.
#   e.g. "Specify one or more upstream ntp servers as an array."
#
#
# === Examples
#
#  class { 'httpd': }
#
# === Authors
#
# Raymond Kristiansen <st02221@uib.no>
#
# === Copyright
#
# Copyright 2013 UiB
#
class httpd (
  $server_admin   = "apache@uib.no",
  $doc_root       = "/var/www/html",
  $replace        = true,
  $server_dns     = $::fqdn,
  $ssl_keys       = $::fqdn,
  $config_dir = $::osfamily ? { RedHat => '/etc/httpd/', default => '', },
  $user = $::osfamily ? { default => 'apache', },
  $group = $::osfamily ? { default => 'apache', },
  $ipv6_addr = $::ipaddress6 ? { undef => false, default => $::ipaddress6 },
  $interface = undef,
  $service = $::osfamily ? {
    Debian => 'www-data',
    RedHat => 'httpd',
    default => '',
  },
  $packages = $::osfamily ? {
    Debian => 'apache2',
    RedHat => 'httpd',
    default => '',
  },
  $prefork_settings = {},
  $listen_ports = { 80 => '' }
)  {

  validate_hash($listen_ports)

  case $interface {
    eth0: { $vhost_ip = $::ipaddress_eth0 }
    eth1: { $vhost_ip = $::ipaddress_eth1 }
    eth2: { $vhost_ip = $::ipaddress_eth2 }
    default: {$vhost_ip = $::ipaddress}
  }

  class { 'httpd::install': } ->
  class { 'httpd::config': } ->
  class { 'httpd::service': }

}
```


Konfigurasjon av applikasjon
```
# == Class: redmine
#
# This install and configures Redmine (http://www.redmine.org)
#
# === Parameters
#
#
# === Authors
#
# Raymond Kristiansen <st02221@uib.no>
#
# === Copyright
#
# Copyright 2013 UiB
#
class redmine(
  $package = undef,
  $user = 'redmine',
  $group = 'redmine',
  $backend = 'sqlite',
  $install_dir = '/var/www/redmine',
  $gemfile = false,
  $bin_path = "/usr/bin",
  $files_symlink = false,
  $email = false,
  $embedded_path = undef
) {

  class { 'redmine::install': } ->
  class { 'redmine::config': }

  if $email {
    class { 'redmine::email':
      require => Class['redmine::config']
    }
  }

}

# Class redmine install
class redmine::install(
  $package = $redmine::package
) {

  if $package {
    package { $package:
      ensure => installed
    }
  }

  # Install ImageMagick
  package { ['ImageMagick', 'ImageMagick-devel']:
    ensure => installed
  }

}
```


Konfigurasjon av spesifikk server
```
---
classes:
  - app::web::redmine
  - motd

authconfig::pam_access: true

redmine::email::host:               'imap.uib.no'
redmine::email::username:           'rts@uib.no'
redmine::email::password:           '`cat /var/www/rts/imap`'
redmine::email::cron:               '*/15'

app::web::redmine::redmine_package: 'rts'
app::web::redmine::install_dir:     '/var/www/rts/redmine'
app::web::redmine::files_symlink:   '/var/www/redmine_files'
```



#### Fordeler

- Provisjoner mye, raskt
- Serveren har akkurat den tilstanden vi ønsker den skal ha
- Endringer i tilstanden kan spores i Git og RTS
- Samme endring i test og produksjon



#### Utrulling av applikasjonen

![Image Alt](http://folk.uib.no/kbo041/devops/images/deployment_av_pakke.png)
<!--![Image Alt](https://www.lucidchart.com/publicSegments/view/55395146-f988-4aea-96ae-474f0a0052f5/image.png)-->


#### Utrulling av applikasjonen

- Applikasjonen pakkes og distribueres som en pakke (rpm)
- Alle avhengigheter er inkludert i pakken
- Uavhengig av krumspring fra upstream
- Full kontroll på kjøremiljøet til applikasjonen
- Server kan oppdateres uten at kjøremiljøet til applikasjonen blir påvirket


#### Oppdatering av applikasjonen

- Utvikleren utvikler, tester og commiter applikasjonen til Git
- Når det er klart til å rulle ut ny versjon av applikasjonen bygges en ny pakke
med utgangspunkt i en Git tag eller commit
- Ny pakke lastes opp til repo og puppet sørger for at den blir installert på de
aktuelle serverene
- Når man skal oppgradere applikasjonen kan man ta opp en ny server med den
nye versjonen og bytte DNS fra eksisterende server til ny, og så kaste den gamle
- Bedre en å prøve å "inplace" oppgradere den eksisterende applikasjonen
- Kan gi oss mindre / ingen nedetid ved oppgradering av applikasjoner




#### Hva ønsker vi å gjøre videre?

- Vi ønsker at flere skal jobbe smartere og ta i bruk verktøy fra verktøykassen
- Automatisert testing av infrastruktur kode
- Automatisert pakking av applikasjoner, f.eks: om en utvikler lager en ny tag i
Git så pakkes og deployes det en ny versjon av applikasjonen



#### Kan devops fungere i en større offentlig institusjon?

- Hvordan skal en få folk med på laget
- Hvordan kan en bygge kompetanse
- Hvordan kan en ta hensyn til at folk har ulik bakgrunn
- Hvordan ta hensyn til at vi er en offentlig bedrift

Er det noen som har innspill så diskuterer vi det gjerne senere idag.


#### Sky / CLoud

- UH-Sky
- IAAS



#### Konklusjon

- Devops for oss er å samarbeide på tvers av grupper og seksjoner
- Devops for oss er å automatisere så mye som mulig
- Devops for oss er å ha versjonskontroll på så mange elementer som mulig
- Devops for oss er å ha gjennomsiktighet, samt dele så mye som mulig
- Devops for oss er å ha empati



#### Spørsmål?

- Interessert i å bruke noen av verktøyene fra verktøykassen?
- Har du noen gode ideer om hvordan IT-Avdelingen kan utvikle seg videre?
- Kan Devops brukes andre steder på UiB?
