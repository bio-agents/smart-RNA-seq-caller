#Base image load
FROM biocontainers/biocontainers:latest

# Metadata
LABEL base.image="biocontainers:latest"
LABEL version="1"
LABEL software="SmartRNASeqCaller"
LABEL software.version="0.1"
LABEL description="SmartRNASeqCaller allows refining VCF calls for germline variants from RNASeq data"
LABEL description="This image comes with all required packages to run the agents in the github repo"
LABEL website=""
LABEL documentation=""
LABEL license=""
LABEL tags="Genomics;Transcriptomics"

# Maintainer
MAINTAINER Mattia Bosio <mattia.bosio@bsc.es>

RUN conda install bcfagents=1.6
RUN conda install tabix
RUN conda install bedagents=2.25.0

RUN conda install pysam=0.13
RUN conda install pandas=0.20.3
RUN conda install -c conda-forge r=3.5.0
# RUN conda install -c conda-forge/label/cf201901 r-caret  
RUN Rscript -e 'install.packages("ranger", repos="http://cran.us.r-project.org")'

WORKDIR /data/

#RUN conda install -c anaconda util-linux
RUN Rscript -e 'install.packages("caret", repos="http://cran.us.r-project.org")'
RUN Rscript -e 'install.packages("e1071", repos="http://cran.us.r-project.org")'

USER root
RUN mkdir -p /opt/SmartRNASeqCaller/

#COPY SmartRNASeqCaller/ /opt/SmartRNASeqCaller/
RUN Rscript -e 'install.packages("optparse", repos="http://cran.us.r-project.org")'
RUN Rscript -e 'install.packages("UpSetR", repos="http://cran.us.r-project.org")'




RUN rm -rf /opt/SmartRNASeqCaller/*
RUN cd /opt; git clone https://github.com/inab/SmartRNASeqCaller.git
RUN cd /opt/SmartRNASeqCaller/resources ; wget https://zenodo.org/record/1473507/files/RNA_Variant_RF_model.rds 
RUN echo 'update'
RUN cd /opt/SmartRNASeqCaller; git pull


USER biodocker
 
