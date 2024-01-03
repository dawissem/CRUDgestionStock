#include <iostream>
#include<string>
#include<fstream>


using namespace std;

const int maxrow = 100;

string id[maxrow] = {};
string name[maxrow] = {};
string qte[maxrow] = {};
string prixUnit[maxrow] = {};

// fonctions de lecture et d'écriture de fichiers pour sauvegarder l'état actuel du stock dans un fichier et pour charger les données au démarrage.
void openFile(){
    string line;
    ifstream myfile("C:\\prod.txt");
    if (myfile.is_open()){
        int x=0;
        while(getline(myfile, line)){
            int l = line.length();
            id[x]= line.substr(0, 4);
            name[x] = line.substr(5, l - 5);
            qte[x] = line.substr(31, 36);
            prixUnit[x] = line.substr(37, l );
            x++;
        }
    }
    else{
        cout<< " On ne peut pas ouvrir le fichier !"<<endl;
    }
}


//tableaux dynamiques pour stocker les informations relatives aux produits, comme le
//nom
//quantité en stock
//prix unitaire
//identifiant unique pour chaque produit.


//Implément des fonctions pour l'ajout d'un nouveau produit au stock,
void AddRecord(){
    char idP[10];
    char nameP[50];
    char qteP[10000];
    char prixUnitP[10];

    cin.ignore(); // pour que pour chaque valeur à saisir il retourne a la ligne

    cout<< "L'identifiant du produit :: ";
    cin.getline(idP,10);

    cout<< "Le nom du produit :: ";
    cin.getline(nameP,50);

    cout<< "La quantite du produit :: ";
    cin.getline(qteP,10000);

    cout<< "Le prix unitaire :: ";
    cin.getline(prixUnitP,10);

    for (int x = 0 ; x < maxrow ; x++){
        if(id[x] =="\0"){
            id[x] = idP;
            name [x] = nameP;
            qte[x] = qteP ;
            prixUnit[x] = prixUnitP;

            break;
        }
    }


}


// modification des quantités,
void updateRecord(string idSearch){
    char idP[10];
    char nameP[50];
    char qteP[10000];
    char prixUnitP[10];

    int counter = 0;

    for ( int x=0 ; x<maxrow ; x++ ){
        if(id[x] == idSearch){
            counter ++ ;
          //  cout << " Le nom du produit : " <<endl ;
          //  cin.getline(nameP,50);
          //  name[x] = nameP;

             cout << " La quantite du produit : " <<endl ;
            cin.getline(qteP,10000);
            qte[x] = qteP;

           //  cout << " Le prix unitaire du produit : " <<endl ;
           // cin.getline(prixUnitP,50);
          //  prixUnit[x] = prixUnitP;

            cout << " * Modification de la quantité avec succes ! *"<<endl;
            cout << "----------------------------------------------------------------\n";
            break;
        }
    }
    if(counter == 0 ){
        cout << "Aucun produit trouve !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }

}

// supprimer un produit definit par l'identifiant
void DeleteRecord( string idSearch){
    int counter =0;

    for ( int x =0 ; x< maxrow ; x++){
        if(id[x]== idSearch){
            counter ++;
            id[x]= "";
            name[x] = "";
            qte[x] = "";
            prixUnit[x] = "";

            cout<< " * Produit a ete supprime avec succes ! * \n "<<endl;
            break;
        }
    }

    if(counter == 0 ){
        cout << "Aucun produit trouve !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }
      cout<<"================================================================"<<endl;

}


//affichage de la liste des produits disponibles.
void ListRecord(){
    system("CLS");
    cout<<"================================================================"<<endl;
    cout << "Le(s) produit(s) disponible(s) sont ::" <<endl;
    cout<<"================================================================"<<endl;

    int counter = 0;
    cout << "Numero  |    ID   |  nom_Produit  |  quantite_Produit  |  prix_Unitaire   "<<endl << "----------------------------------------------------------------\n";
    for (int x=0 ; x< maxrow ; x++){
        if(id[x]!="\0"){
            counter ++ ;
            cout << "  " << counter << "  " << id[x] << "   " << name[x] <<  "   " << qte[x] << "   " << prixUnit[x] <<endl ;
            cout << "---------------------------------------------------------------\n";
        }
    }
    if(counter == 0 ){
        cout << "Aucun produit n'est disponible !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }
      cout<<"================================================================"<<endl;


}

//recherche permettant aux utilisateurs de trouver des produits par nom
void searchNameRecord(string nameSearch){
    system("CLS");
    cout << "Le(s) produit(s) disponible(s) sont ::" <<endl;
    cout<<"================================================================"<<endl;

    int counter =0;
    for (int x=0 ; x< maxrow ; x++){
        if(name[x] == nameSearch){
            counter ++ ;
            cout << "  " << counter << "  " << id[x] << "   " << name[x] <<  "   " << qte[x] << "   " << prixUnit[x] <<endl ;
            cout << "----------------------------------------------------------------\n";
            break;
        }
    }
    if(counter == 0 ){
        cout << "Aucun produit trouve !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }
      cout<<"================================================================"<<endl;


}


//recherche permettant  de trouver des produits par  prix,
void searchPriceRecord(string prixSearch){
    system("CLS");
    cout << "Le(s) produit(s) disponible(s) sont ::" <<endl;
    cout<<"================================================================"<<endl;

    int counter =0;
    for (int x=0 ; x< maxrow ; x++){
        if(prixUnit[x] == prixSearch){
            counter ++ ;
            cout << "  " << counter << "  " << id[x] << "   " << name[x] <<  "   " << qte[x] << "   " << prixUnit[x] <<endl ;
            cout << "----------------------------------------------------------------\n";
            break;
        }
    }
    if(counter == 0 ){
        cout << "Aucun produit trouve !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }
      cout<<"================================================================"<<endl;


}

//recherche permettant  de trouver des produits par quantité en stock.
void searchQteRecord(string qteSearch){
    system("CLS");
    cout << "Le(s) produit(s) disponible(s) sont ::" <<endl;
    cout<<"================================================================"<<endl;

    int counter =0;
    for (int x=0 ; x< maxrow ; x++){
        if(qte[x] == qteSearch){
            counter ++ ;
            cout << "  " << counter << "  " << id[x] << "   " << name[x] <<  "   " << qte[x] << "   " << prixUnit[x] <<endl ;
            cout << "----------------------------------------------------------------\n";
            break;
        }
    }
    if(counter == 0 ){
        cout << "Aucun produit trouve !\n"<<endl;
        cout << "----------------------------------------------------------------\n";
    }
      cout<<"================================================================"<<endl;


}



//******************************************************
//******************************************************


//******************************************************
//******************************************************

void saveToFile(){
    ofstream myfile ;
    myfile.open("D:\\prod.txt");

    for(int x= 0 ; x < maxrow ; x++){
        if(id[x] == "\0"){
            break;
        }
        else{
            myfile << id[x] +"," + name[x] +"," + qte[x] +"," +prixUnit[x] << endl;
        }
    }
}

int main()
{
    cout << "Menu\n" << endl;
    int option;
    string id;
    string name;
    string qte;
    string prixUnit;
    system("CLS");
    openFile();

    cout<<"==============================================================================="<<endl;
        cout<<"=========Projet : Systeme de Gestion de Stock  Fait par MANAI Wissem========="<<endl;


    do{
    cout<<"================================================================================="<<endl;
    cout<< "-1- Ajouter un nouveau produit au stock" << endl; // create Records
    cout<< "-2- Modifier les quantites d'un produit donne" << endl; // update Records
    cout<< "-3- Supprimer un produit donne" << endl; // Delete Records
    cout<< "-4- Rechercher des produits par NOM " << endl; // Search records NOM
    cout<< "-5- Rechercher des produits par PRIX " << endl; // Search records PRIX
    cout<< "-6- Rechercher des produits par QUANTITE DE STOCK " << endl; // Search records QTE STOCK
    cout<< "-7- Afficher la liste des produits disponibles" << endl; // display all Records
    cout<< "-8- Quitter et sauvegarder l'etat actuel du stock dans un fichier" << endl; // Exit and save to Textfile
    cout<<"================================================================"<<endl;
    cout<< "                    Choisir une option                    "<< endl;
    cout<<"================================================================"<<endl;

    cin >> option;

    switch(option){
        case 1: AddRecord();
            system("CLS");
            break;

        case 2:
            cin.ignore();
            cout<<"Modifier la quantite d'un produit par l'identifiant ID :: ";
            getline(cin,id);
            updateRecord(id);
            break;

        case 3:
            cin.ignore();
            cout << "Supprimer un produit par l'identifiant ID :: ";
            getline(cin,id);
            DeleteRecord(id);
            system("CLS");
            break;

        case 4:
            cin.ignore();
            cout << "Rechercher d'un produit par NOM :: ";
            getline(cin, name);
            searchNameRecord(name);
            break;

       case 5:
            cin.ignore();
            cout << "Rechercher d'un produit par PRIX :: ";
            getline(cin, prixUnit);
            searchPriceRecord(prixUnit);
            break;

        case 6:
            cin.ignore();
            cout << "Rechercher d'un produit par QUANTITE DE STOCK :: ";
            getline(cin, qte);
            searchQteRecord(qte);
            break;



        case 7: ListRecord();
            break;
   }
    } while( option != 8 );
    saveToFile();
    cout << "Quitter ... Sauveguarder dans le fichier"<<endl;
// affichage cout il faut choisir entre 1 et 6
return 0;
}
