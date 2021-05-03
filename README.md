# nhap-xuat
#include <stdio.h>
#include <string.h>
#include <conio.h>

struct ThucUong{
    char ten[30];
    char loai[30];
    int giatien;
};

void nhap(ThucUong &TU){
	fflush(stdin);
	printf("\nTen thuc uong: ");
    gets(TU.ten);
    printf("Loai thuc uong: ");
    gets(TU.loai);
    printf("Nhap gia tien thuc uong: ");
    scanf("%d", &TU.giatien);
}

void xuat(ThucUong TU){
	printf("%-20s %-20s %-15d \n", TU.ten, TU.loai, TU.giatien);
}
void nhapDuLieu(ThucUong TU[], int &n){
    printf("Nhap so luong thuc uong: ");
    scanf("%d", &n);
    for(int i = 0; i<n; i++){
    	printf("Nhap thong tin thuc uong %d: \n", i);
    	nhap(TU[i]);
    }
}
void xuatDuLieu(ThucUong TU[], int n){
	printf("\n --------- Thong tin thuc uong -----\n");
    printf("%-20s %-20s %-20s\n", "Ten thuc uong", "Loai" , "Gia tien");
    for (int i=0; i<n; i++){
        xuat(TU[i]);
    }
}
//Sap xep thong tin theo the loai (Z-A)
void SapXepTheoTheLoai(ThucUong TU[], int n){
	ThucUong t;
	for(int i=0; i<n; i++){
		for(int j=i+1; j<n; j++){
			if(strcmp(TU[i].loai, TU[j].loai)<0){
				t=TU[i];
				TU[i]=TU[j];
				TU[j]=t;
			}
		}
	}
}

//Thong ke theo the loai
void ThongKe(ThucUong TU[], int n){
	int dem=0;
	for(int i=0; i<n; i++){
		dem++;
		if(strcmp(TU[i].loai, TU[i+1].loai)!=0){
			printf("**%s co %d thuc uong!\n", TU[i].loai, dem);
			dem=0;
		}
	}
}

//Tim kiem theo the loai
void TimKiem(ThucUong TU[], char LoaiTU[], int n){
	for(int i=0; i<n; i++){
		if(strcmp(LoaiTU, TU[i].loai)==0)
			xuat(TU[i]);
		else
			printf("Khong co thuc uong nao thuoc loai nay!");
	}
}

int main(){
    struct ThucUong TU[100];
    char LoaiTU[20];
    int n;
    nhapDuLieu(TU, n);
    xuatDuLieu(TU, n);
    printf("Thong tin thuc uong sau khi sap xep la: \n");
    SapXepTheoTheLoai(TU, n);
    xuatDuLieu(TU, n);
    printf("\nThong ke theo the loai: \n");
    ThongKe(TU, n);
    fflush(stdin);
	printf("\nNhap loai thuc uong can tim: ");
	gets(LoaiTU);
    TimKiem(TU, LoaiTU, n);
}
