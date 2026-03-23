########### TMHMM v2.0 ###########
# mac、linux版本均可
tar zxvf tmhmm-2.0d.macOS.tar.gz
cd tmhmm-2.0d
# 修改: ./bin/tmhmm 和 ./bin/tmhmmformat.pl 的第一行perl路径
cat ../Pythium_ultimum.pug.pep.all.fa | ../bin/tmhmm > pu_tmhmm.out
####################################

########### SignalP v5.0 ###########
tar zxvf signalp-5.0b.Linux.tar.gz
cd signalp-5.0b
mkdir -p ~/local/bin
mkdir -p ~/local/lib
cp ./bin/signalp ~/local/bin/
cp -r ./lib ~/local/
echo 'export PATH=$HOME/local/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
signalp -h
signalp \
    -fasta Pythium_ultimum.pug.pep.all.fa \
    -org euk \
    -format short \
    -gff3 \
    -mature \
    -prefix pu.signalp_out
####################################
