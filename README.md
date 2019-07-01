# utl-populating-a-numeric-array-based-on-character-string-without-a-loop
    Populating a numeric array based on character string without a loop                                                
                                                                                                                       
          AB++++B+BD+A++BCDB++++B++A+B++A++BC++B+B+D                                                                   
                                                                                                                       
          For each of the 42 characers define 42 element numeric array where                                           
                                                                                                                       
            "+'=1                                                                                                      
             all other characters=0                                                                                    
                                                                                                                       
         Two Solutions                                                                                                 
                                                                                                                       
             a. input @@  by                                                                                           
                Bartosz Jablonski                                                                                      
                yabwon@gmail.com                                                                                       
                                                                                                                       
             b. translate prx                                                                                          
                                                                                                                       
                                                                                                                       
    github                                                                                                             
    https://tinyurl.com/y2692vpe                                                                                       
    https://github.com/rogerjdeangelis/utl-populating-a-numeric-array-based-on-character-string-without-a-loop         
                                                                                                                       
    SAS Forum                                                                                                          
    https://tinyurl.com/y28tr58a                                                                                       
    https://communities.sas.com/t5/SAS-Programming/how-to-use-macro-variable-in-array-do-loop/m-p/570303               
                                                                                                                       
    *_                   _                                                                                             
    (_)_ __  _ __  _   _| |_                                                                                           
    | | '_ \| '_ \| | | | __|                                                                                          
    | | | | | |_) | |_| | |_                                                                                           
    |_|_| |_| .__/ \__,_|\__|                                                                                          
            |_|                                                                                                        
    ;                                                                                                                  
                                                                                                                       
     items="AB++++B+BD+A++BCDB++++B++A+B++A++BC++B+B+D";                                                               
                                                                                                                       
    *            _               _                                                                                     
      ___  _   _| |_ _ __  _   _| |_                                                                                   
     / _ \| | | | __| '_ \| | | | __|                                                                                  
    | (_) | |_| | |_| |_) | |_| | |_                                                                                   
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                  
                    |_|                                                                                                
    ;                                                                                                                  
                                                                                                                       
                                                                                                                       
    Up to 40 obs from WANT total obs=1                                                                                 
                                                                                                                       
    Obs   NUM1   NUM2   NUM3   NUM4   NUM5 ...   NUM40   NUM41   NUM42                                                 
                                                                                                                       
     1      0      0      1      1      1  ...     0       1       0                                                   
                                                                                                                       
                              RULES                                                                                    
                              |                                                                                        
    Variable Type    Value    |                                                                                        
                              |                                                                                        
    NUM1      N8       0      |  A=0                                                                                   
    NUM2      N8       0      |  B=0                                                                                   
    NUM3      N8       1      |  +=1                                                                                   
    NUM4      N8       1      |  +=1                                                                                   
    NUM5      N8       1      |  +=1                                                                                   
    ...                                                                                                                
    ...                                                                                                                
    NUM35     N8       0      |                                                                                        
    NUM36     N8       1      |                                                                                        
    NUM37     N8       1      |                                                                                        
    NUM38     N8       0      |                                                                                        
    NUM39     N8       1      |                                                                                        
    NUM40     N8       0      |                                                                                        
    NUM41     N8       1      |                                                                                        
    NUM42     N8       0      |                                                                                        
                              |                                                                                        
    *          _       _   _                                                                                           
     ___  ___ | |_   _| |_(_) ___  _ __                                                                                
    / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                               
    \__ \ (_) | | |_| | |_| | (_) | | | |                                                                              
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                              
                                                                                                                       
    ;                                                                                                                  
                                                                                                                       
    *           _                   _        ____    ____                                                              
      __ _     (_)_ __  _ __  _   _| |_     / __ \  / __ \                                                             
     / _` |    | | '_ \| '_ \| | | | __|   / / _` |/ / _` |                                                            
    | (_| |_   | | | | | |_) | |_| | |_   | | (_| | | (_| |                                                            
     \__,_(_)  |_|_| |_| .__/ \__,_|\__|   \ \__,_|\ \__,_|                                                            
                       |_|                  \____/  \____/                                                             
    ;                                                                                                                  
                                                                                                                       
    proc format;                                                                                                       
      invalue fmt (default=1)                                                                                          
      "+" = 1                                                                                                          
      other = 0                                                                                                        
      ;                                                                                                                
    run;                                                                                                               
                                                                                                                       
    data have;                                                                                                         
    infile cards;                                                                                                      
    input x fmt1. @@;                                                                                                  
    line + (mod(_N_,80)=0);                                                                                            
    if 0<mod(_N_,80)<43;                                                                                               
    cards;                                                                                                             
    AB++++B+BD+A++BCDB++++B++A+B++A++BC++B+B+D                                                                         
    AB++++B+BD+A++BCDB++++B++A+B++A++BC++B+B+D                                                                         
    ++++++++++++++++++++++++++++++++++++++++++                                                                         
    ABCDABCDABCDABCDABCDABCDABCDABCDABCDABCDAB                                                                         
    ;                                                                                                                  
    run;                                                                                                               
                                                                                                                       
    proc transpose data = have out = want(drop=_:) prefix=x;                                                           
    by line;                                                                                                           
    run;                                                                                                               
                                                                                                                       
    *_         _                       _       _                                                                       
    | |__     | |_ _ __ __ _ _ __  ___| | __ _| |_ ___                                                                 
    | '_ \    | __| '__/ _` | '_ \/ __| |/ _` | __/ _ \                                                                
    | |_) |   | |_| | | (_| | | | \__ \ | (_| | ||  __/                                                                
    |_.__(_)   \__|_|  \__,_|_| |_|___/_|\__,_|\__\___|                                                                
                                                                                                                       
    ;                                                                                                                  
                                                                                                                       
    %symdel len ary / nowarn;                                                                                          
                                                                                                                       
    proc daasets lib=work;                                                                                             
    delete want;                                                                                                       
    run;quit;                                                                                                          
                                                                                                                       
    data _null_;                                                                                                       
                                                                                                                       
      length ary $200;                                                                                                 
                                                                                                                       
      items="AB++++B+BD+A++BCDB++++B++A+B++A++BC++B+B+D";                                                              
      items=translate(translate(items,'0000',"ABCD"),"1","+");                                                         
                                                                                                                       
      ary=prxchange('s/(\d)(?=\d)/$1,/',-1,items);                                                                     
                                                                                                                       
      call symputx('ary',ary);                                                                                         
      call symputx('len',length(items));                                                                               
                                                                                                                       
      rc=dosubl('                                                                                                      
         data want;                                                                                                    
            array numd[&len] num1-num42 (&ary);                                                                        
            output;                                                                                                    
         run;quit;                                                                                                     
      ');                                                                                                              
                                                                                                                       
     stop;                                                                                                             
    run;quit;                                                                                                          
                                                                                                                       
                                                                                                                       
