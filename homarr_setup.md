# proxmox intergration

1. go to proxmox GUI > node name > system > certificates
2. click on the certificate "hostname-root-ca.pem" (eg. pve-root-ca.pem) > view certificate > expand "raw certificate"
3. copy the raw certificate and paste it into a text editor/notepad
   - for mac make sure to change the format to plaintext: format > make plain text (or shift + command + T)
4. add ".crt" to the file eg.

   `hostname-root-ca.pem.crt`

5. in homarr, click on your profile picture > your preferences > tools > certificates and upload your certificate
6. still in "your preferences", go to intergrations > new intergration > search "proxmox"
7. follow steps in sources link
8. you may be prompted to trust the certificate or that the hostname mistmatch, trust both and then click "test connection and create"
   - if trusting one of the options has an infinite loading animation popup box, close this and click "test connection and create"

## sources

- https://homarr.dev/docs/integrations/proxmox/
