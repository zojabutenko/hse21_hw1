# hse21_hw1

[Link to google colab](https://colab.research.google.com/drive/1FvOz4lRgoQNpk4xyoPWzYrv2VLAQ97Gw?usp=sharing)

# All commands used:
## creating soft links in my directory:

$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq oil_R1.fastq

$ ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq oil_R2.fastq

$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq oilMP_S4_L001_R1_001.fastq

$ ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq

## getting random samples:

*5 mil of paired-end:*

$ seqtk sample -s1406 oil_R1.fastq 5000000 > sub1.fastq

$ seqtk sample -s1406 oil_R2.fastq 5000000 > sub2.fastq

*1.5 mil of mate-pairs:*

$ seqtk sample -s1406 oilMP_S4_L001_R1_001.fastq 1500000 > sub3.fastq

$ seqtk sample -s1406 oilMP_S4_L001_R2_001.fastq 1500000 > sub4.fastq


## evaluate using fastqc:

$ fastqc /home/zabutenko/sub1.fastq

$ fastqc /home/zabutenko/sub2.fastq

$ fastqc /home/zabutenko/sub3.fastq

$ fastqc /home/zabutenko/sub4.fastq

## move files to a dir to do fastqc:

$ mkdir fastqc

$ mv sub1_fastqc.html sub1_fastqc.zip sub2_fastqc.html sub2_fastqc.zip sub3_fastqc.html sub3_fastqc.zip sub4_fastqc.html sub4_fastqc.zip fastqc

## do multiqc:

$ cd fastaqc

$ multiqc -o . .

## cut adapters:

$ cd /home/zabutenko/

$ platanus_trim  sub1.fastq sub2.fastq

$ platanus_internal_trim sub3.fastq sub4.fastq

## evaluate cut files using fastqc:

$ fastqc sub1.fastq.trimmed

$ fastqc sub2.fastq.trimmed

$ fastqc sub3.fastq.int_trimmed

$ fastqc sub4.fastq.int_trimmed

## evaluate cut files using multiqc:

$ multiqc -o . .

## remove uncut files:

$ rm sub1.fastq sub2.fastq sub3.fastq sub4.fastq

## assemble:

$ time platanus assemble -o Poil -t 8 -m 28 -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log

## scaffold:

$ time platanus scaffold -o Poil -t 8 -c  Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 sub3.fastq.int_trimmed sub4.fastq.int_trimmed 2> scaffold.log

## close gaps:

$ time platanus gap_close -o Poil -t 8 -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 sub3.fastq.int_trimmed sub4.fastq.int_trimmed 2> scaffold.log

# Screenshots:
## of original reads:
![Снимок экрана 2021-12-05 в 06 34 54](https://user-images.githubusercontent.com/55627796/144732475-c7141d59-3b11-4c73-8433-ee2f89463a5a.png)
![Снимок экрана 2021-12-05 в 06 35 27](https://user-images.githubusercontent.com/55627796/144732477-23a18f35-d6ee-4990-b965-88b536f73ef8.png)
![Снимок экрана 2021-12-05 в 06 35 40](https://user-images.githubusercontent.com/55627796/144732479-eadaf845-a941-4a15-9181-4461f5f5fdd8.png)
![Снимок экрана 2021-12-05 в 06 36 39](https://user-images.githubusercontent.com/55627796/144732483-03c4918b-4203-4a34-b96c-851610e8b74e.png)
![Снимок экрана 2021-12-05 в 06 36 39](https://user-images.githubusercontent.com/55627796/144732517-d252f150-dd79-41d5-b7cf-726216005ba7.png)
![Снимок экрана 2021-12-05 в 06 36 47](https://user-images.githubusercontent.com/55627796/144732486-98487517-e21a-4a26-a006-f693f16f5688.png)
![Снимок экрана 2021-12-05 в 06 36 55](https://user-images.githubusercontent.com/55627796/144732490-522574e2-036f-4291-a27b-198e36e1bd5e.png)
![Снимок экрана 2021-12-05 в 06 37 16](https://user-images.githubusercontent.com/55627796/144732496-fe126b8d-fddb-49d3-ab3c-29e1a7b05109.png)
![Снимок экрана 2021-12-05 в 06 37 16](https://user-images.githubusercontent.com/55627796/144732523-ac9327b9-e5db-4a47-b072-b4969a44af29.png)
![Снимок экрана 2021-12-05 в 06 37 26](https://user-images.githubusercontent.com/55627796/144732501-885d1ce7-7eb6-4352-bdf9-29565785ddfc.png)

## of trimmed reads:
![Снимок экрана 2021-12-05 в 06 42 33](https://user-images.githubusercontent.com/55627796/144732597-20a8ec0a-0862-4fbb-b02d-bd95faca69be.png)
![Снимок экрана 2021-12-05 в 06 42 40](https://user-images.githubusercontent.com/55627796/144732599-b38aea00-193b-4cdf-beed-98be9231fa26.png)
![Снимок экрана 2021-12-05 в 06 42 48](https://user-images.githubusercontent.com/55627796/144732606-b412a752-406c-4180-be09-90347d185965.png)
![Снимок экрана 2021-12-05 в 06 43 50](https://user-images.githubusercontent.com/55627796/144732616-4ef86830-4beb-4ad9-8aaf-2f23c8369cfd.png)
![Снимок экрана 2021-12-05 в 06 43 42](https://user-images.githubusercontent.com/55627796/144732617-127b85e8-04fb-4348-a302-9c18a0812fb4.png)
![Снимок экрана 2021-12-05 в 06 43 34](https://user-images.githubusercontent.com/55627796/144732618-df8c7974-bd17-47d3-a7fe-4cc7859d2d3b.png)
![Снимок экрана 2021-12-05 в 06 43 27](https://user-images.githubusercontent.com/55627796/144732619-b5f46353-ff6b-47c6-8641-6b4fdc9f78cb.png)
![Снимок экрана 2021-12-05 в 06 43 19](https://user-images.githubusercontent.com/55627796/144732621-3c5c7bc1-96d3-42dc-b9de-0ea4bc0dd49b.png)
![Снимок экрана 2021-12-05 в 06 43 12](https://user-images.githubusercontent.com/55627796/144732623-5ceb8661-18be-4f88-852a-c0a1055e75fa.png)
![Снимок экрана 2021-12-05 в 06 43 03](https://user-images.githubusercontent.com/55627796/144732624-912235d6-d5ef-469d-83d7-fac2ccdab122.png)
![Снимок экрана 2021-12-05 в 06 42 55](https://user-images.githubusercontent.com/55627796/144732625-130e1174-c924-4b81-b3ad-2233d5c5fd18.png)


