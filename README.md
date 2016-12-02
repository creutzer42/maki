# maki
#include <iostream>
#include <math.h>
#include <string>
#include <algorithm>

using namespace std;

class Branche{
    double a,b;
public:
    Branche(double a_i,double b_i){
        a=a_i;
        b=b_i;
    }

};


class Maki{
    double x,y,V;
    int alpha;
    string name;
public:
    Maki(double x0, string Name){
        name=Name;
        x=x0;
    };
    Maki(double x0, double y0,double V0,int alpha0, string Name){
        name=Name;
        x=x0;
        y=y0;
        V=V0;
        alpha=alpha0;
    };

/*    Maki Saut_maki(Maki M, Branches B){
        x=cos(alpha)*V0*t+x0;
        y=sin(alpha)*V0*t+y0-5*pow(t,2);
    };*/

};

Maki place_maki(Maki M, Branche Br,double x0){
    double a,b;
    double y0=a*x0+b; //j'arrive pas à faire en sorte qu'il comprenne que c'est le y du maki
    return M;

};
double Temps_Branche(Maki M,Branche Br){
    double a,b,V,y,x,t1,t2,t;
    int alpha;
    /* x=cos(alpha)V0t+x0, y=sin(alpha)V0t+y0-1/2*g(t^2),or y=ax+b
    => y=y, sin(alpha)V0t+y0-1/2*g(t^2) = ax+b = a*(cos(alpha)V0t+x0)+b
    => (sin(alpha)-a*cos(alpha))*V0*t+(y0-a*x0-b)-1/2*g*(t^2)=0
    => B*t+C+A(t^2)*/
    double A=(-5); //g=10
    double B=(sin(alpha)-a*cos(alpha))*V;
    double C=y-(a*x)-b;
    double D=pow(B,2)-4*A*C; //détermient
    t1 = ((-B)+sqrt(D))/(2*A);
    t1 = ((-B)-sqrt(D))/(2*A);
    if (D>0) t=fmin(t1,t2); //sol double
    else if (D==0) t=(-B)/(2*A); //sol unique
    else
        cout << "game over !";
        t=0;
    return t;

};
int main()
{
    string Name="bob";
    double x=0,a=3,b=4;
    double y0;
    Maki M(x,"bob");
    Branche Br(a,b);
    place_maki(M,Br,x);
    Branche Br2(0,2);
    M =M(x,y0,5/*La vitesse*/,0.7/*l'angle de saut en radiant*/,Name)//ça casse ici :/
    //J'arrive pas à réutiliser l'objet M de la classe maki pour le rebalancer dans ma fonction calcul de temps du saut
    Temps_Branche(M,Br);
    //comment je fais pour utiliser les variable d'un objet de classe Maki?
    return 0;
}
