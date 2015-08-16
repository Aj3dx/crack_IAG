# crack_IAG
keyes md5, sh1


	

    #!/usr/bin/python
    import os,sys,re,hashlib,urllib2,string
    class CrackNet():
     
      def __init__(self):
        pass
      YELLOW = '\033[93m'
      global key    
      global pwd
      global user  
      global wordlist
      global help
      global work    
    def banner():
       print CrackNet.YELLOW + '''
          ____                _    _   _      _       _  _  ___    _    ____
         / ___|_ __ __ _  ___| | _| \ | | ___| |_   _| || ||_ _|  / \ / ___|
        | |   | '__/ _` |/ __| |/ /  \| |/ _ \ __| |_  ..  _| |  / _ \| |  _
        | |___| | | (_| | (__|   <| |\ |  __/ |_  |_      _| | / ___ \ |_| |
         \____|_|  \__,_|\___|_|\_\_| \_|\___|\__|   |_||_||___/_/   \_\____|
                                                                             
                               _____                    
                              |_   _|__  __ _ _ __ ___  
                                | |/ _ \/ _` | '_ ` _ \
                                | |  __/ (_| | | | | | |
                                |_|\___|\__,_|_| |_| |_|
                                                       
     
           ''' + CrackNet.YELLOW
     
     
    def Grab():
     
      target_url = sys.argv[1]
      for line in urllib2.urlopen(target_url):
            grab = line
     
      k = grab.find("#")
      p = grab.find("$")
      u = grab.find("@")
      w = grab.find("*")
      if k != -1 and p != -1 and u != -1  and w != -1:
              print "Configurazione corrette"
      else:
            print "Configurazione errate"
      key = grab[k+1:p-1]
      pwd = grab[p+1:u-1]
      user = grab[u+1:w-1]
      wordlist = grab[w+1:len(grab)]
      print "L'operatore: " + user + "\nHa richiesto una collaborazione per la chiave: " + pwd + "\nTipologia: " + key + "\n"
      help = raw_input("Confermare la collaborazione?? Y/N: ")
     
    def chklength(hashes):
        if len(hashes) != 32:
            print("[-] Improper length for md5 hash")
            sys.exit(1)
     
    def attacca():
        hashes = pwd
        chklength(hashes)
        chiave = key
        wordlist = raw_input("\nInserisci il percorso file della wordlist: ")
        try:
            words = open(wordlist, "r")
        except(IOError):
            print("[-] Si e' verificato un errore nel percorso file.\n")
            sys.exit(1)
        words = words.readlines()
        print "\nWordlist caricata con successo.... parole caricate: ",len(words)
        for word in words:
            h  = hashlib.new(chiave)
            h.update(word[:-1])
            value = h.hexdigest()
            if hashes == value:
                print"[+] Password Trovata:  " + word
                sys.exit(0)
     
    def getwordlist():
       url =  wordlist
       bashCommand = "wget " + url + " -O wlist.txt"
       os.system(bashCommand)
     
     
    def main()
      work = raw_input("1 - Crea obbiettivo\n2 - collabora con il team")
      if work == "1":
          #split()
      else:
            Grab()
            if help == "Y":
                   getwordlist()
                   attacca()
     
    banner()
    main()

