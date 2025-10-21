# Image officielle Apache httpd
FROM httpd:2.4-alpine

COPY conf/httpd.conf /usr/local/apache2/conf/httpd.conf
# Copie la landing page dans le dossier servi par défaut
COPY public-html/ /usr/local/apache2/htdocs/

