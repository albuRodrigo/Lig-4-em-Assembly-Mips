# Lig-4-em-Assembly-Mips
.data
matriz: .word 0:64 #--crio uma matriz [8] [8] chea de 0


.text

la $a0, matriz #----Salvo endereço da matriz

li $s0, 0x00FF0000 #--vermelho

li $s1, 0x00000000 #--preto

li $s2, 0xFFFFFFFF #--- branco

li $a1, 0x10010000#---endereço tela mars


#---pintar um quadrado-----

funcão_local_disponivel: #---procurar o 0(zero) mais baixo
#---- $a1 ----- tela mars
#---- $a2 ----- é a coluna que o usuairo que colocar
#---- $a3 ----- é par ou impar, pra ver quem é o jogador
#---- $a0 ----- é a matriz, pro calculo base
li $t1, 7 #--ultima linha
addi $a1,$a1,-1 #---- faço a correção de dados, aqui vai de 0....7


procura:
#-------------- achar endereço
mul $t2, $t1,8
add $t2,$t2,$a2
mul $t2,$t2,4
add $t2,$t2, $a0
#--------------
lw $t3,0($t2) #----salvo em $t3 o valor correspondete ao espaço 

beq $t3,$zero,prencher #---- se tiver vazio
addi $t1,$t1,-1 #---subo uma coluna
bltz  $t1,acabou  #---se a coluna ta toda cheia
j procura#--se não prencheu nem acabou eu continuo procurando

prencher:
#------------ calcular resto se par = jogador 1, se impar jogador 2
rem $t5,$a3,2 
#-------------

#-----------procurar endereço correspondete ao do bitmap

#---------------

sub $t4,$t2,$a0 # salvo em $t4, a diiferença do valor base da matriz e do encontrado
add $t4,$t4,$a1 # $t4, tem a diferença mas o valor do bitmap


beq $t5,0,par
beq $t5,1,impar




par:
sw $s0,0 ($t4)
sw $s0,0 ($t2)

jr $ra

impar:
sw $s2,0($t4)
sw $s2, 0($t2)

jr $ra
