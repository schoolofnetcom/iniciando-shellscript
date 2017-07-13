#!/bin/bash
# Exemplo Final de Script Shell
#
 
Principal() {
  echo "Exemplo Final sobre o uso de scripts shell"
  echo "------------------------------------------"
  echo "Op��es:"
  echo
  echo "1. Trasformar nomes de arquivos"
  echo "2. Adicionar um usu�rio no sistema"
  echo "3. Deletar um usu�rio no sistema"
  echo "4. Fazer backup dos arquivos do /etc"
  echo "5. Sair do exemplo"
  echo
  echo -n "Qual a op��o desejada? "
  read opcao
  case $opcao in
    1) Transformar ;;
    2) Adicionar ;;
    3) Deletar ;;
    4) Backup ;;
    5) exit ;;
    *) "Op��o desconhecida." ; echo ; Principal ;;
  esac
}
 
Transformar() {
  echo -n "Para Mai�sculo ou min�sculo? [M/m] "
  read var
  if [ $var = "M" ]; then
    echo -n "Que diret�rio? "
    read dir
 
    for x in `/bin/ls` $dir; do
      y=`echo $x | tr '[:lower:]' '[:upper:]'`
      if [ ! -e $y ]; then
        mv $x $y
      fi
    done
 
  elif [ $var = "m" ]; then
    echo -n "Que diret�rio? "
    read dir
 
    for x in `/bin/ls` $dir; do
      y=`echo $x | tr '[:upper:]' '[:lower:]'`
      if [ ! -e $y ]; then
        mv $x $y
      fi
    done
 
  fi
}
 
Adicionar() {
  clear
  echo -n "Qual o nome do usu�rio a se adicionar? "
  read nome
  adduser nome
  Principal
}
 
Deletar() {
  clear
  echo -n "Qual o nome do usu�rio a deletar? "
  read nome
  userdel nome
  Principal
}
 
Backup() {
  for x in `/bin/ls` /etc; do
    cp -R /etc/$x /etc/$x.bck
    mv /etc/$x.bck /usr/backup
  done
}
 
Principal
