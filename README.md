# Issues when installing pyrouge following the steps below:

### Steps to solve issues when installing pyrouge!

#### If you find any more issues other than these steps or better ways to solve these issues, feel free to create a pull request and send me an [email here](muraliraghubabu1994@gmail.com].

Follow the below instructions:

1) install pyrouge using the command from [here](https://pypi.python.org/pypi/pyrouge/0.1.0):  
```
pip install pyrouge
```    

2) Download the Rouge-1.5.5 folder from [here](https://github.com/andersjo/pyrouge/tree/master/tools/ROUGE-1.5.5):    
```
https://github.com/andersjo/pyrouge/tree/master/tools/ROUGE-1.5.5
```

3) Now set the pyrouge path appropriately using this:   
```
pyrouge_set_rouge_path /absolute/path/to/ROUGE-1.5.5/directory
```  


4) Now, test the following code:

```
from pyrouge import Rouge155

r = Rouge155()
r.system_dir = 'path/to/system_summaries'
r.model_dir = 'path/to/model_summaries'
r.system_filename_pattern = 'some_name.(\d+).txt'
r.model_filename_pattern = 'some_name.[A-Z].#ID#.txt'

output = r.convert_and_evaluate()
print(output)
output_dict = r.output_to_dict(output)
``` 

```
- If the above steps work, then great, else the below steps might be useful.
```  

5) If the error is soemthing like: ```can't locate XML/parser.pm in @INC ubuntu ...``` 
Found a solution [here](https://www.experts-exchange.com/questions/23188990/Error-Can't-locate-XML-Parser-pm-in-INC-Perl-CentOS.html)
Then, you need to download the XML::Parser from CPAN here: http://search.cpan.org/~msergeant/XML-Parser-2.44/
```
wget -r -np -R "index.html*" http://search.cpan.org/CPAN/authors/id/T/TO/TODDR/XML-Parser-2.44.tar.gz
tar -xzf XML-Parser-2.44.tar.gz
cd XML-Parser-2.44 
perl Makefile.PL
```

6) If the error is something like: ```Can't locate LWP/UserAgent.pm in @INC ubuntu ...```
then follow the link [here](https://help.directadmin.com/item.php?id=274) for the next steps:
```
perl -MCPAN -e 'install Bundle::LWP'
```
or 
```
wget http://www.cpan.org/modules/by-module/LWP/libwww-perl-5.837.tar.gz
tar xvzf libwww-perl-5.837.tar.gz
cd libwww-perl-5.837
perl Makefile.PL
make
make install
```

7) If the error is something like: ```Cannot open exception db file for reading:``` 
then run the following steps:    
```
cd pyrouge/ROUGE-1.5.5/data/
rm WordNet-2.0.exc.db
./WordNet-2.0-Exceptions/buildExeptionDB.pl ./WordNet-2.0-Exceptions ./smart_common_words.txt ./WordNet-2.0.exc.db
```



The following links helped: [Link 1](https://pypi.python.org/pypi/pyrouge/0.1.0),[Link 2](https://github.com/bheinzerling/pyrouge),
[Link 3](https://stackoverflow.com/questions/47045436/how-to-install-the-python-package-pyrouge-on-microsoft-windows/47045437#47045437),
[Link 4](https://github.com/andersjo/pyrouge),
[Link 5](https://github.com/tagucci/pythonrouge/issues/4).




pyrouge
=======

A Python interface to the ROUGE package.

Right now, only the basic functionality is in place. You can score one summary at a time with respect to multiple reference summaries.
Down the road, the plan is to reimplement (parts of) ROUGE in pure Python.
The motivation is that the ROUGE package, while standard in evaluation of extractive summaries,
can be a challenge to obtain and install, and also does not fit well in a Python workflow.

Contributions and suggestions are very welcome.

## Usage example

```
from pyrouge import Rouge155
from pprint import pprint

ref_texts = {'A': "Poor nations pressurise developed countries into granting trade subsidies.",
             'B': "Developed countries should be pressurized. Business exemptions to poor nations.",
             'C': "World's poor decide to urge developed nations for business concessions."}
summary_text = "Poor nations demand trade subsidies from developed nations."


rouge = Rouge155(n_words=100)
score = rouge.score_summary(summary_text, ref_texts)
pprint(score)
```

The output will be this:

```
{'rouge_1_f_score': 0.76879,
 'rouge_1_f_score_cb': 0.76879,
 'rouge_1_f_score_ce': 0.76879,
 'rouge_1_precision': 0.86928,
 'rouge_1_precision_cb': 0.86928,
 'rouge_1_precision_ce': 0.86928,
 'rouge_1_recall': 0.68912,
 'rouge_1_recall_cb': 0.68912,
 'rouge_1_recall_ce': 0.68912,
 'rouge_2_f_score': 0.52941,
 'rouge_2_f_score_cb': 0.52941,
 'rouge_2_f_score_ce': 0.52941,
 'rouge_2_precision': 0.6,
 'rouge_2_precision_cb': 0.6,
 'rouge_2_precision_ce': 0.6,
 'rouge_2_recall': 0.47368,
 'rouge_2_recall_cb': 0.47368,
 'rouge_2_recall_ce': 0.47368,
 'rouge_3_f_score': 0.39521,
 'rouge_3_f_score_cb': 0.39521,
 'rouge_3_f_score_ce': 0.39521,
 'rouge_3_precision': 0.44898,
 'rouge_3_precision_cb': 0.44898,
 'rouge_3_precision_ce': 0.44898,
 'rouge_3_recall': 0.35294,
 'rouge_3_recall_cb': 0.35294,
 'rouge_3_recall_ce': 0.35294,
 'rouge_4_f_score': 0.34147,
 'rouge_4_f_score_cb': 0.34147,
 'rouge_4_f_score_ce': 0.34147,
 'rouge_4_precision': 0.38889,
 'rouge_4_precision_cb': 0.38889,
 'rouge_4_precision_ce': 0.38889,
 'rouge_4_recall': 0.30435,
 'rouge_4_recall_cb': 0.30435,
 'rouge_4_recall_ce': 0.30435,
 'rouge_su4_f_score': 0.61313,
 'rouge_su4_f_score_cb': 0.61313,
 'rouge_su4_f_score_ce': 0.61313,
 'rouge_su4_precision': 0.6977,
 'rouge_su4_precision_cb': 0.6977,
 'rouge_su4_precision_ce': 0.6977,
 'rouge_su4_recall': 0.54685,
 'rouge_su4_recall_cb': 0.54685,
 'rouge_su4_recall_ce': 0.54685}
```
## Run tests

The unit tests can be run be issuing ``nosetests´´ from the root directory of the package.
