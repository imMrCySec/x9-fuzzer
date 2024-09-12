# x9-Fuzzer

<p align="center">
  <a href="#requirements">Requirements</a> •
  <a href="#installation">Installation</a> •
  <a href="#tool-options">Tool options</a> •
  <a href="#usage">Usage</a> •
  <a href="#license">license</a>
</p>

URL Fuzzing Tool. Developed By MrCySec. https://x.com/mrcysec

## Requirements
- Python3

## Installation
  1. `git clone https://github.com/imMrCySec/x9-fuzzer.git`
  2. `cd x9-fuzzer`
  2. `chmod +x main.py`
  4. `python3 main.py -h`
  
## Note
- You can also add path of the tool to your bash or zsh profile to run it everywhere by add the flowing line in `.profile`
- `alias x9="python3 ~/x9-fuzzer/main.py"`
- Now you can run tool in every directory
- `x9 -h`


## Tool Options
- `-u` or `--url` : Single URL to edit
- `-l` or `--url_list` : File with links (not used with -u)
- `-p` or `--parameters` : File with parameters (required for 'ignore', 'normal', and 'all' strategies)
- `-c` or `--chunk` : Number of parameters per URL (default: 25)
- `-v` or `--values_inline` : Values provided inline
- `-vf` or `--values_file` : File with values (ignored if -vf is provided)
- `-gs` or `--generate_strategy` : Select the mode strategy from the available choice, choices=['ignore', 'combine', 'normal', 'all']
	`normal` : Remove all parameters and put the wordlist
	`combine` : Pitchfork combine on the existing parameters
	`ignore` : Don't touch the URL and put the wordlist
	`all` : All in one method
- `-vs` or `--value_strategy` : Value strategy (required for 'combine'), choices=['replace', 'suffix']
	`replace` : Replace the value with gathered value
	`suffix` : Append the value to the end of the parameters
- `-o` or `--output` : File to save the output (default: x9-generated-link.txt)
- `-s` or `--silent` : Silent mode
- `-h` or `--help` : Display help message

## Usage

Single URL :
```
python3 main.py -u "https://domain.tld/?param1=value1&param2=value2" -gs all -vs suffix -v '"MAMAD"' -p param.txt -c 20

Output:

https://domain.tld/?param1=value1%22MAMAD%22&param2=value2
https://domain.tld/?param1=value1&param2=value2%22MAMAD%22
https://domain.tld/?param1=value1&param2=value2&hidden_param1=%22MAMAD%22&hidden_param2=%22MAMAD%22
https://domain.tld/?hidden_param1=%22MAMAD%22&hidden_param2=%22MAMAD%22

```

List of URLs :
```
python3 main.py -l urls.txt -gs all -vs suffix -v '"MAMAD"' -p param.txt -c 20

Output:

https://domain.tld/?param1=value1%22MAMAD%22&param2=value2
https://domain.tld/?param1=value1&param2=value2%22MAMAD%22
https://domain.tld/?param1=value1&param2=value2&hidden_param1=%22MAMAD%22&hidden_param2=%22MAMAD%22
https://domain.tld/?hidden_param1=%22MAMAD%22&hidden_param2=%22MAMAD%22

```

Multiple value as payload
```
python3 main.py -u "https://domain.tld/?param1=value1&param2=value2" -gs all -vs suffix -v '"MAMAD"'  "'MAMAD'"  '<b/MAMAD' -p param.txt -c 20
```

List of values as payload
```
python3 main.py -u "https://domain.tld/?param1=value1&param2=value2" -gs all -vs suffix -vf value.txt -p param.txt -c 20
```

Run the tool in silent mode
```
python3 main.py -u "https://domain.tld/?param1=value1&param2=value2" -gs all -vs suffix -v '"MAMAD"'  "'MAMAD'"  '<b/MAMAD' -p param.txt -c 20 -s
```

Write output to a file
```
python3 main.py -u "https://domain.tld/?param1=value1&param2=value2" -gs all -vs suffix -v '"MAMAD"'  "'MAMAD'"  '<b/MAMAD' -p param.txt -c 20 -o output.txt
```

## License
This project is licensed under the MIT license. See the LICENSE file for details.
