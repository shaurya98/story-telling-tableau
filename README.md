# story-telling-tableau
LIBNAME mydata "/courses/d1406ae5ba27fe300 " access=readonly;
data new; set mydata.gapminder;

label  incomeperperson = 'Income_per_person'
       internetuserate = 'Internet_use_rate'
       urbanrate = 'Urban_rate'
       GIPP = 'group income per person'
       GIUR = 'group internet use rate'
       GUR = 'group urban rate';
if incomeperperson eq . then gipp= . ;
else if incomeperperson LE 744.239 then gipp = 1;
else if incomeperperson LE 9425.36 then gipp = 2;
else if incomeperperson GT 9425.36 then gipp =3;

if gipp NE .;

proc sort; by country;
proc sort; by gipp;
proc corr; var urbanrate internetuserate;by gipp;
run;
