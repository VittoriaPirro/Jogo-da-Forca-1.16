//Declaração das bibliotecas
#include <stdio.h>
#include <stdlib.h>
#include <windows.h>
#include <time.h>
#include <string.h>
#include <ctype.h>

//Declaração das variavéis globais
    int menu;
    int x2 = 0;
    int x1 = 0;
    int x;
    int c; /* contador   */
    int i; /* contador   */
    int z;
    char palavras[200] = "";
    int ascii[20];
    int palavras1;
    int status_palavra = 0;
    int tam_palavra_inserida;
    char palavra_real[20] = "";
    char palavra_secreta[20] = "";
    char letra1[20];
    int main_engine = 1;
    int engine;
    int exit_code;
    int ui;
    int dificuldade ;
    int vida = 6;
    int erros;
    int acertos_erros[50];
    char letras_erradas[13];
    char stick1[3]= " ";
    char stick2[3]= " ";
    char stick3[3]= " ";
    char stick4[3]= " ";
    char stick5[3]= " ";
    char stick6[3]= " ";
    char key1[5] = "menu";
    char espacos[100];
    char vidas[18] = "<3 <3 <3 <3 <3 <3 ";
    char espacos1[100] = "          ";
    char espacos2[100] = "               ";


//Função para a animação de morte, usando contador de erros de 0-6 (coraçõeszinhos)
void death_animation(){
    if ( erros == 0){
        if ( dificuldade != 0){
            strcpy(espacos1, "          ");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, "           ");
        }
    }
    if ( erros == 1 ){
        strcpy(stick1, "o");
        strcpy(vidas, "<3 <3 <3 <3 <3    ");
        if ( dificuldade != 0){
            strcpy(espacos1, "        ");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, "         ");
        }
    }
    if ( erros == 2 ){
        strcpy(stick2, "|");
        strcpy(vidas, "<3 <3 <3 <3       ");
         if ( dificuldade != 0){
            strcpy(espacos1, "      ");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, "       ");
        }
    }
    if ( erros == 3 ){
        strcpy(stick3, "/");
        strcpy(vidas, "<3 <3 <3          ");
         if ( dificuldade != 0){
            strcpy(espacos1, "    ");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, "     ");
        }
    }
    if ( erros == 4 ){
        strcpy(stick4, "\\");
        strcpy(vidas, "<3 <3             ");
         if ( dificuldade != 0){
            strcpy(espacos1, "  ");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, "   ");
        }
    }
    if ( erros == 5 ){
        strcpy(stick5, "/");
        strcpy(vidas, "<3                ");
         if ( dificuldade != 0){
            strcpy(espacos1, "");
        }
        if ( dificuldade == 0){
            strcpy(espacos1, " ");
        }
    }
    if ( erros == 6 ){
        strcpy(stick6, "\\");

    }
}
//Função para resetar todas  as variáveis declaradas anteriormente
void reset_all(){
     menu = "";
     x1 = 0;
     x2 = 0;
     x = 0;
     c = 0;
     i = 0;
     tam_palavra_inserida = 0;
     palavra_real[20] = "";
     palavra_secreta[20] = "";
     letra1[20] = "";
     status_palavra = 0;
     engine = 1;
     exit_code;
     ui = 1;
     vida = 6;
     erros = 0;
     acertos_erros[50] = "";
     strcpy(letras_erradas, " ");
     strcpy(stick1, " ");
     strcpy(stick2, " ");
     strcpy(stick3, " ");
     strcpy(stick4, " ");
     strcpy(stick5, " ");
     strcpy(stick6, " ");
     strcpy(vidas, "<3 <3 <3 <3 <3 <3 ");
     key1[5] = "menu";
     espacos[100] = "";
     char espacos1[100] = "         ";
}
// Ve se o codigo binario é "000...0", se sim significa que a palavra não existe. O "i" é um contador.
void num_erro(){
    i = 0;
    for (c = 0; c < tam_palavra_inserida; c++){
        if ( acertos_erros[c] == 1){
            i = i + 1;
        }
        if ( acertos_erros[c] == 0){
            i = (i + 2);
        }
    }
    for ( c = 0; c < tam_palavra_inserida; c++){
        acertos_erros[c] = 0;
    }
        if ( i == (2*tam_palavra_inserida)){
            erros = erros + 1;
            strncat(letras_erradas, letra1, 1);
            strncat(letras_erradas, " ", 2);
        }
}
//Função para forçar a saída, interrompe o loop atual para redirecionar a função
void exit_codes(){
    if (exit_code == 001){
        loose();
    }
    if (exit_code == 002){
        win();
    }
    if (exit_code == 005){
        menu = 1;
    }
}
//Função gera o numero de espaços para os colocar dentro doquadrado impresso na main
void palavra_codigo(){
    x = 0;
    x = 29 - ((tam_palavra_inserida * 2) - 1);
    if ( dificuldade != 2 ){
        x = x - 6;
    }
    if ( dificuldade == 2){
        x = x - 6;
    }
    for ( c = 0; c <= x; c++){
        strcat(espacos, " ");
    }
    printf(" |                                                               ");
    for (c = 0; c < tam_palavra_inserida; c++){
        printf(" %c",palavra_secreta[c]);
    }
    printf("%s", espacos);
    printf("__|__    |");
    printf("\n");
    strcpy(espacos,"");
}
// Animação para win
void win(){
    system("cls");
    printf("YYYYYYY       YYYYYYY     OOOOOOOOO     UUUUUUUU     UUUUUUUU     WWWWWWWW                           WWWWWWWWIIIIIIIIIINNNNNNNN        NNNNNNNN \n");
    printf("Y:::::Y       Y:::::Y   OO:::::::::OO   U::::::U     U::::::U     W::::::W                           W::::::WI::::::::IN:::::::N       N::::::N \n");
    printf("Y:::::Y       Y:::::Y OO:::::::::::::OO U::::::U     U::::::U     W::::::W                           W::::::WI::::::::IN::::::::N      N::::::N \n");
    printf("Y::::::Y     Y::::::YO:::::::OOO:::::::OUU:::::U     U:::::UU     W::::::W                           W::::::WII::::::IIN:::::::::N     N::::::N \n");
    printf("YYY:::::Y   Y:::::YYYO::::::O   O::::::O U:::::U     U:::::U       W:::::W           WWWWW           W:::::W   I::::I  N::::::::::N    N::::::N \n");
    printf("   Y:::::Y Y:::::Y   O:::::O     O:::::O U:::::D     D:::::U        W:::::W         W:::::W         W:::::W    I::::I  N:::::::::::N   N::::::N \n");
    printf("    Y:::::Y:::::Y    O:::::O     O:::::O U:::::D     D:::::U         W:::::W       W:::::::W       W:::::W     I::::I  N:::::::N::::N  N::::::N \n");
    printf("     Y:::::::::Y     O:::::O     O:::::O U:::::D     D:::::U          W:::::W     W:::::::::W     W:::::W      I::::I  N::::::N N::::N N::::::N \n");
    printf("      Y:::::::Y      O:::::O     O:::::O U:::::D     D:::::U           W:::::W   W:::::W:::::W   W:::::W       I::::I  N::::::N  N::::N:::::::N \n");
    printf("       Y:::::Y       O:::::O     O:::::O U:::::D     D:::::U            W:::::W W:::::W W:::::W W:::::W        I::::I  N::::::N   N:::::::::::N \n");
    printf("       Y:::::Y       O:::::O     O:::::O U:::::D     D:::::U             W:::::W:::::W   W:::::W:::::W         I::::I  N::::::N    N::::::::::N \n");
    printf("       Y:::::Y       O::::::O   O::::::O U::::::U   U::::::U              W:::::::::W     W:::::::::W          I::::I  N::::::N     N:::::::::N \n");
    printf("       Y:::::Y       O:::::::OOO:::::::O U:::::::UUU:::::::U               W:::::::W       W:::::::W         II::::::IIN::::::N      N::::::::N \n");
    printf("    YYYY:::::YYYY     OO:::::::::::::OO   UU:::::::::::::UU                 W:::::W         W:::::W          I::::::::IN::::::N       N:::::::N \n");
    printf("    Y:::::::::::Y       OO:::::::::OO       UU:::::::::UU                    W:::W           W:::W           I::::::::IN::::::N        N::::::N \n");
    printf("    YYYYYYYYYYYYY         OOOOOOOOO           UUUUUUUUU                       WWW             WWW            IIIIIIIIIINNNNNNNN         NNNNNNN \n");
    printf("                                                                                                                                                \n\n");
    printf("                                                                                                                                                \n");
    main_engine = 1;
}
// Animação para loose
void loose(){
    system("cls");
    printf("  A palavra era ** %s **\n\n", palavra_real);
    printf("                                                                                                                                                \n\n");

    printf("YYYYYYY       YYYYYYY                                     LLLLLLLLLLL                  OOOOOOOOO        SSSSSSSSSSSSSSS EEEEEEEEEEEEEEEEEEEEEE \n");
    printf("Y:::::Y       Y:::::Y                                     L:::::::::L                OO:::::::::OO    SS:::::::::::::::SE::::::::::::::::::::E \n");
    printf("Y:::::Y       Y:::::Y                                     L:::::::::L              OO:::::::::::::OO S:::::SSSSSS::::::SE::::::::::::::::::::E \n");
    printf("Y::::::Y     Y::::::Y                                     LL:::::::LL             O:::::::OOO:::::::OS:::::S     SSSSSSSEE::::::EEEEEEEEE::::E \n");
    printf("YYY:::::Y   Y:::::YYYooooooooooo   uuuuuu    uuuuuu         L:::::L               O::::::O   O::::::OS:::::S              E:::::E       EEEEEE\n");
    printf("   Y:::::Y Y:::::Y oo:::::::::::oo u::::u    u::::u         L:::::L               O:::::O     O:::::OS:::::S              E:::::E              \n");
    printf("    Y:::::Y:::::Y o:::::::::::::::ou::::u    u::::u         L:::::L               O:::::O     O:::::O S::::SSSS           E::::::EEEEEEEEEE   \n");
    printf("     Y:::::::::Y  o:::::ooooo:::::ou::::u    u::::u         L:::::L               O:::::O     O:::::O  SS::::::SSSSS      E:::::::::::::::E   \n");
    printf("      Y:::::::Y   o::::o     o::::ou::::u    u::::u         L:::::L               O:::::O     O:::::O    SSS::::::::SS    E:::::::::::::::E   \n");
    printf("       Y:::::Y    o::::o     o::::ou::::u    u::::u         L:::::L               O:::::O     O:::::O       SSSSSS::::S   E::::::EEEEEEEEEE   \n");
    printf("       Y:::::Y    o::::o     o::::ou::::u    u::::u         L:::::L               O:::::O     O:::::O            S:::::S  E:::::E             \n");
    printf("       Y:::::Y    o::::o     o::::ou:::::uuuu:::::u         L:::::L         LLLLLLO::::::O   O::::::O            S:::::S  E:::::E       EEEEEE\n");
    printf("       Y:::::Y    o:::::ooooo:::::ou:::::::::::::::uu     LL:::::::LLLLLLLLL:::::LO:::::::OOO:::::::OSSSSSSS     S:::::SEE::::::EEEEEEEE:::::E \n");
    printf("    YYYY:::::YYYY o:::::::::::::::o u:::::::::::::::u     L::::::::::::::::::::::L OO:::::::::::::OO S::::::SSSSSS:::::SE::::::::::::::::::::E \n");
    printf("    Y:::::::::::Y  oo:::::::::::oo   uu::::::::uu:::u     L::::::::::::::::::::::L   OO:::::::::OO   S:::::::::::::::SS E::::::::::::::::::::E \n");
    printf("    YYYYYYYYYYYYY    ooooooooooo       uuuuuuuu  uuuu     LLLLLLLLLLLLLLLLLLLLLLLL     OOOOOOOOO      SSSSSSSSSSSSSSS   EEEEEEEEEEEEEEEEEEEEEE \n");
    printf("                                                                                                                                                \n\n");

    printf("                                                |===-~___                _,-'\n");
    printf("                 -==\\                         `//~\\   ~~~~`---.___.-~~     \n");
    printf("             ______-==|                         | |  \\           _-~`       \n");
    printf("       __--~~~  ,-/-==\\                        | |   `\        ,'           \n");
    printf("    _-~       /'    |  \\                      / /      \      /              \n");
    printf("  .'        /       |   \\                   /' /        \   /'              \n");
    printf(" /  ____  /         |    \`\.__/-~~ ~ \ _ _/'  /          \/'                \n");
    printf("/-'~    ~~~~~---__  |     ~-/~         ( )   /'        _--~`                 \n");
    printf("                  \_|      /        _)   ;  ),   __--~~                      \n");
    printf("                    '~~--_/      _-~/-  / \   '-~ \                          \n");
    printf("                   {\__--_/}    / \\_>- )<__\      \                         \n");
    printf("                   /'   (_/  _-~  | |__>--<__|      |                        \n");
    printf("                  |0  0 _/) )-~     | |__>--<__|     |                       \n");
    printf("                  / /~ ,_/       / /__>---<__/      |                        \n");
    printf("                 o o _//        /-~_>---<__-~      /                         \n");
    printf("                 (^(~          /~_>---<__-      _-~                          \n");
    printf("                ,/|           /__>--<__/     _-~                             \n");
    printf("             ,//('(          |__>--<__|     /                  .----_        \n");
    printf("            ( ( '))          |__>--<__|    |                 /' _---_~\      \n");
    printf("         `-)) )) (           |__>--<__|    |               /'  /     ~\`\    \n");
    printf("        ,/,'//( (             \__>--<__\    \            /'  //        ||    \n");
    printf("      ,( ( ((, ))              ~-__>--<_~-_  ~--____---~' _/'/        /'     \n");
    printf("    `~/  )` ) ,/|                 ~-_~>--<_/-__       __-~ _/                \n");
    printf("  ._-~//( )/ )) `                    ~~-'_/_/ /~~~~~~~__--~                  \n");
    printf("   ;'( ')/ ,)(                            ~~~~~~~~~~                       \n");
    printf("  ' +----------+                                                            \n");
    printf("    |    `     |                                                              \n");
    printf("    |          |                                                            \n");
    printf("    O          |                                                            \n");
    printf("   /|\          |                                                           \n");
    printf("   / \          |                                                           \n");
    printf("               |                                                          \n");

}
//Função que lê e sorteia o arquivo
void ler_arquivo(){
    srand(time(NULL));
    while ( status_palavra !=1 ){
        x2 = 0;
        z = rand() %5000;
        FILE * fp = fopen("palavras.txt", "r"); //abre o arquivo
        for ( c = 0; c < z; c++){
            fscanf(fp, "%s", palavras);
        }
        tam_palavra_inserida = strlen(palavras); //atribui para tam_palavra_inserida
        switch (dificuldade){ //seleciona a dificuldade
        case 0:
            if ( tam_palavra_inserida == 4){
                x1 = 1;
            }
            break;
        case 1:
            if ( tam_palavra_inserida == 5){
                x1 = 1;
            }
            break;
        case 2:
            if ( tam_palavra_inserida >= 6){
                x1 = 1;
            }
            break;
        }
        if ( x1 == 1){
            for ( c = 0; c < tam_palavra_inserida; c++){ //limitar apenas para simbolos de a-z
                x1 = 0;
                ascii[c] = palavras[c];
                if (ascii[c] < 123){
                    x1 = 0;
                    if (ascii[c] > 96){
                        x2 = x2 + 1;
                    }
                }
            }
        }
        if ( x2 == tam_palavra_inserida ){
            strcpy(palavra_real, palavras);
            status_palavra = 1;
        }
        fclose(fp);
    }
    tam_palavra_inserida = strlen(palavra_real);
    for ( c = 0; c < tam_palavra_inserida; c++){
        palavra_secreta[c] ='_'; //Gerar  "_" para cada letra
    }
}
// Função Interface para mostrar a dificuldade na interface da função main
void print_dificuldade1(){
    switch (dificuldade){
        case 0:
            printf(" | Dificuldade: Facil *                                                                             |");
            break;
        case 1:
            printf(" | Dificuldade: Media  **                                                                           |");
            break;
        case 2:
            printf(" | Dificuldade: Dificil ***                                                                         |");
            break;
        default:
            printf("-------------");
            break;
    }
}
//Função para mostrar associar a  dificuldade no menu
void print_dificuldade(){
    switch (dificuldade){
        case 0:
            printf("Facil");
            break;
        case 1:
            printf("medio");
            break;
        case 2:
            printf("dificil");
            break;
        default:
            printf("-------------");
            break;
    }
}
//Função que desenha o menu da dificuldade
void menu_dificuldade(){
    printf(" _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ \n");
    printf("|                                                                                                 |\n");
    printf("|                                       Forca v1.13                                               | \n");
    printf("|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|\n\n");
    printf("                                   ESCOLHA A DIFICULDADE                                     \n");
    printf("\n                                     0)     FACIL                                         \n\n");
    printf("\n                                     1)     MEDIO                                         \n\n");
    printf("\n                                     2)    DIFICIL                                         \n\n");
    scanf("");
    scanf("%d", &dificuldade); // leitura da dificuldade

}
//Função que desenha o primeiro menu
void menu_principal(){
    system("cls");
    status_palavra = 0;
    ler_arquivo();
    system("cls");
    printf(" _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ \n");
    printf("|                                                                                                 |\n");
    printf("|                                       Forca v1.13                                               | \n");
    printf("|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|\n\n");
    printf("                                      MENU PRINCIPAL                                     \n");
    printf("\n                                  1)       Jogar                                       \n");
    printf("\n                                  2)    Dificuldade                                       \n");
    printf("\n                                  3)     Creditos                                        \n");
    printf("\n                                  4)       Sair                                         \n");
    printf("\n\n");
    printf("Dificuldade selecionada: ");
    print_dificuldade();
    printf("\n");
    scanf("%d", &menu);
}
//Função que desenha tela de creditos
void creditos(){
    system("cls");
    printf(" _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ \n");
    printf("|                                                                                                 |\n");
    printf("|                                       Forca v1.13                                               | \n");
    printf("|_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|\n\n");
    printf("                                         CREDITOS                                     \n");
    printf("\n\n");
    printf("                               Desenvolvimento:_____________Vittoria                              \n\n");
    printf("                               Art&design:__________________Vittoria                                  \n\n");
    printf("                               Acabamento:__________________Vittoria                                            \n\n");
    printf("\n\n\n\n\n\n\n\n\n\n\n");
    system("pause");
}
//Função principal
int main(void){
    while (main_engine == 1){
        if (exit_code != 005){
            menu_principal();
        }
        switch (menu){ //estrutura do menu
            case 1:
                engine = 1;
                erros = 0;
                i = 0;
                ui = 1;
                for ( c = 0; c < 50; c++){
                    acertos_erros[c] = 0;
                }
                system("cls");
                printf("\n");
                ler_arquivo(); //chama a função ler arquivo

                while ( ui == 1) { //controle do quadrado
                    system("cls");
                    death_animation(); //chama a função dos <3 <3 <3 <3 <3 <3
                    if ( erros != 6 ) {
                        engine = 1;
                    }
                    printf("\n\n\n\n");
                    printf("                                                           Insira \"menu\" para voltar para o menu \n");
                    printf(" +-------------------------------------------------------------------------------------------------+\n");
                    printf(" | Vidas: %s%s                                                        |\n", vidas, espacos2);
                    print_dificuldade1();
                    printf("\n");
                    printf(" |                                                                               +----------+      |\n");
                    printf(" |                                                                               |          |      |\n");
                    printf(" |                                                                               |          |      |\n");
                    printf(" |                                                                               %s          |      |\n", stick1);
                    printf(" |                                                                              %s%s%s         |      |\n", stick3, stick2, stick4);
                    printf(" |                                                                              %s %s         |      |\n", stick5, stick6);
                    printf(" |                                                                                          |      |\n");
                    printf(" |                                                                                          |      |\n");
                    printf(" |  Tentativas anteriores:                                                                  |      |\n");
                    printf(" |      %s%s                                                                         |      |\n", letras_erradas, espacos1);
                    palavra_codigo(); //chama palavra codigo
                    printf(" |                                                                                       /     \\   |\n");
                    printf(" |                                                                                      /_______\\  |\n");
                    printf(" +-------------------------------------------------------------------------------------------------+\n");
                    printf("                            ");
                    if ( erros == 6 ){
                        ui = 0;
                        exit_code = 001;
                    }
                    if ( strcmp(palavra_real,palavra_secreta) == 0){
                        exit_code = 002;
                        engine = 0;
                        ui = 0;
                    }
                    while ( engine == 1 && erros < 6 ){
                        engine = 0;
                        printf("          ");
                        printf(" digite uma letra     ");
                        scanf("%s", &letra1);
                        printf("\n");
                        if ( strcmp(letra1, key1) == 0 ){
                            engine = 0;
                            ui = 0;
                        }
                        for (c = 0; c <= tam_palavra_inserida; c++){
                            if ( letra1[0] == palavra_real[c]){
                            palavra_secreta[c] = letra1[0];
                            acertos_erros[c] = 1;
                            }
                        }
                        num_erro();
                    }
                }
                exit_codes(); // Chama função de saída
                printf("\n\n");
                system("pause");
                break;
            case 2:
                system("cls");
                menu_dificuldade();
                break;
            case 3:
                creditos();
                break;
            case 4:
                system("cls");
                printf(" IT IS DANGEROUS TO GO ALONE, TAKE THIS! \n");

                 printf("\n\n\n");
                printf("              (O)               \n");
                printf("              <M                \n");
                printf("   o          <M                \n");
                printf("  /| ......  /:M\------------------------------------------------,,,,,,   \n");
                printf("(O)[]XXXXXX[]I:K+}=====<{H}>================================------------> \n");
                printf("  \| ^^^^^^  \:W/------------------------------------------------''''''   \n");
                printf("   o          <W                                                          \n");
                printf("              <W                                                          \n");
                printf("              (O)                                                         \n");
                printf("\n\n\n\n");
                system("pause");
                main_engine = 0;
                break;
            break;
            default:
                printf("\nerror 000000x4\nInvalid input\nProcess will be terminated.\n");
                main_engine = 0;
                break;
            }
            reset_all();
        }
}
