# QipsiusPsychology

---

Example to generate localhost wildcard

    $ openssl req -newkey rsa:2048 -x509 -nodes -keyout wildcard_qpsycology_dev.key -new -out wildcard_qpsycology_dev.crt -subj /CN=*.qpsycology.dev -reqexts SAN -extensions SAN -config <(cat /System/Library/OpenSSL/openssl.cnf <(printf '[SAN]\nsubjectAltName=DNS:*.qpsycology.dev')) -sha256 -days 3650

