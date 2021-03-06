FITS testing tool
======================

A tool to test the [File Information Tool Set (FITS)](https://code.google.com/p/fits/) against a test corpora.
This tool will allow to pass a FITS implementation by argument and test it against a set of files, producing and report on Microsoft Excel format. Optionally, you can pass a ground truth file which will be used to validate the FITS output results in terms of mime type, puid and validation.

## Build & Use

To build the application simply clone the project and execute the following Maven command: `mvn clean package`  
The binary will appear at `target/fits-testing-1.0-SNAPSHOT-jar-with-dependencies.jar`

To see the usage options execute the command:

```bash
$ java -jar target/fits-testing-1.0-SNAPSHOT-jar-with-dependencies.jar -h
usage: report
 -d <arg>   directory with files to process
 -f <arg>   fits home
 -g <arg>   ground truth file
 -h         print this message
 -o <arg>   output file
```

To test a FITS against the included corpora, execute the following command:

```bash
$ java -jar target/fits-testing-1.0-SNAPSHOT-jar-with-dependencies.jar -d corpora/files/ -f ../fits-harvard-lts/ -g corpora/groundtruth.xls -o results/results-fits-harvard-lts.xls
```

Note that this command assumes you have downloaded the harvard-lts version of FITS into the parent folder.

## Results

These are test results that resulted from the execution of this tool against several FITS versions.

| Repository | [harvard-lts](https://github.com/harvard-lts/fits)                                                | [openplanets](https://github.com/openplanets/fits)                                                | [openplanets](https://github.com/openplanets/fits)                                                 | [keeps](https://github.com/keeps/fits)                                                       |
|:-----------|--------------------------------------------------------------------------------------------------:|--------------------------------------------------------------------------------------------------:|---------------------------------------------------------------------------------------------------:|---------------------------------------------------------------------------------------------:|
| **Branch** | [master](https://github.com/harvard-lts/fits/tree/master)                                         | [master](https://github.com/openplanets/fits/tree/master)                                         | [gary-master](https://github.com/openplanets/fits/tree/gary-master)                                | [keeps](https://github.com/keeps/fits/tree/keeps)                                            |
| **Commit** | [0a1cd57f22](https://github.com/harvard-lts/fits/commit/0a1cd57f22c24f1c8be7ab75607628058505b961) | [2ff3bc2dc0](https://github.com/openplanets/fits/commit/2ff3bc2dc06b05cb9bbbe6778eae80a36743cd51) | [7b0c2dd4c2](https://github.com/openplanets/fits/commit/7b0c2dd4c23e0900192fbe4dd6802bfae59a13df)  | [6fcb46a03c](https://github.com/keeps/fits/commit/6fcb46a03c3c19d8b19c4040553e19f02c76f89f)  |
| **% correct<sup>1</sup> MIME type**     |  35.4% |  35.4% |    25% |  62.5% |
| **% incorrect<sup>1</sup> MIME type**   |  60.4% |  64.6% |  70.8% |  33.3% |
| **% unknown<sup>1</sup> MIME type**     |   4.2% |     0% |   4.2% |   4.2% |
| **% correct PUID**                      |    25% |    25% |     0% |  66.7% |
| **% incorrect PUID**                    |   4.2% |   4.2% |     0% |  20.8% |
| **% unknown PUID**                      |  70.8% |  70.8% |   100% |  12.5% |
| **% correct validation<sup>2</sup>**    |   2.1% |   2.1% |   2.1% |   2.1% |
| **% incorrect validation<sup>2</sup>**  |     0% |     0% |     0% |     0% |
| **% unknown validation<sup>2</sup>**    |  33.3% |  33.3% |  22.9% |  64.6% |
| **Avg. extracted features**             |    8.3 |    8.3 |    8.4 |    8.8 |
| **Avg. exec. time (ms)**                |   3731 |   3692 |   2324 |   5609 |
| **Results spreadsheet** | [download](results/harvard_01112013.xls) | [download](results/openPlanets_01112013.xls) | [download](results/gary_01112013.xls) | [download](results/keeps_01112013.xls) |

<sup>1</sup> Correct result is one that agrees with the ground truth, incorrect result is one that disagrees with the ground truth, and unknown result is one where FITS gives no answer.  
<sup>2</sup> The validation depends on the identification process. A tool will try to validate a file against the format it has identified, so if the identification is wrong, the validation cannot be considered as correct. So we only count validations of correct identifications (of MIME type or PUID), but the result is divided by the total number of files. This is why the total number of correct, incorrect and unknown validations in not 100%.



Test date: 2013-11-01  
Test environment:
* Processor: Intel® Core™ i5 CPU 650 @ 3.20GHz × 4
* Memory: 7.7 GiB
* Disk: Western Digital WD Black WD1002FAEX 1TB 7200 RPM 64MB Cache SATA 6.0Gb/s
* Operative system: Ubuntu 12.04.3 LTS
* Java virtual machine: OpenJDK 1.6.0_27

Corpora:
* Provided [files](corpora/files) with manually created [ground truth](corpora/groundtruth.xls)
* 48 files
* Formats:
 * Vector graphics: Adobe Illustrator, Corel Draw
 * Text, spreadsheet and presentation: Microsoft Office and Libre Office
 * Application data: Lotus Notes

## License

This software is available under the [LGPL version 3 license](LICENSE). All corpora was created specifically for this project and is available under the [Creative Commons Attribution-ShareAlike 3.0 Unported License](http://creativecommons.org/licenses/by-sa/3.0/deed.en_US").



