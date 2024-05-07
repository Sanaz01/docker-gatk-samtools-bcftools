# build as vortexing/gatk-samtools-bcftools:4.1.8.0-1.10-1.9
FROM broadinstitute/gatk:4.1.8.0
		
RUN curl --insecure https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

## Remove pre-installed samtools from GATK		
RUN apt purge -y samtools

RUN apt-get update && \
	apt-get install -y zlib1g-dev libncurses5-dev libbz2-dev liblzma-dev libcurl4-openssl-dev && \
    rm -rf /var/lib/apt/lists/*

# Add on samtools
WORKDIR /
RUN wget -q --no-check-certificate https://github.com/samtools/samtools/releases/download/1.10/samtools-1.10.tar.bz2 && \
	tar jxf samtools-1.10.tar.bz2 && \
	rm samtools-1.10.tar.bz2 && \
	cd samtools-1.10 && \
	make 
ENV PATH=${PATH}:/samtools-1.10

# Add on bcftools
WORKDIR /
RUN wget -q --no-check-certificate https://github.com/samtools/bcftools/releases/download/1.9/bcftools-1.9.tar.bz2 && \
	tar jxf bcftools-1.9.tar.bz2 && \
	rm bcftools-1.9.tar.bz2 && \
	cd bcftools-1.9 && \
	make install

WORKDIR /gatk