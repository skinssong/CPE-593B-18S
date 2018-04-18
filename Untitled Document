import java.util.Random;

public class Matrix {
    private int size;
    private double[][] arr;
    private double[] target;

    public Matrix(int n){
        Random r = new Random();
        size = n;
        arr = new double[n][n];
        for (int i=0; i<n; i++){
            for (int j=0; j<n; j++){
                arr[i][j] = 0;
            }
        }
        target = new double[n];
        for (int j=0;j<n;j++){
            target[j]=0;
        }
    }

    public void set_matrix_element(int i, int j, double element){
        this.arr[i][j] = element;
    }

    public void set_target_element(int i, double element){
        this.target[i] = element;
    }

    public int pivoting(int start_row, int start_col){
        double max = this.arr[start_row][start_col];
        int max_row = start_row;

        for (int row=start_row+1; row<this.size;row++){
            if (this.arr[row][start_col]>max){
                max = this.arr[row][start_col];
                max_row = row;
            }
        }

        return max_row;
    }

    public void swap(int a, int b){
        if (a != b) {
            for (int col = 0; col < this.size; col++) {
                double temp = this.arr[a][col];
                this.arr[a][col] = this.arr[b][col];
                this.arr[b][col] = temp;
            }
            double temp2 = this.target[a];
            this.target[a] = this.target[b];
            this.target[b] = temp2;
        }
    }

    public void reduce(int start_row, int start_col) {
        int to_swap_row = pivoting(start_row, start_col);
        swap(start_row, to_swap_row);

        for (int row = start_row + 1; row < this.size; row++) {
            double ratio = this.arr[row][start_col] / this.arr[start_row][start_col];
            for (int col = start_col; col < this.size; col++) {
                this.arr[row][col] = this.arr[row][col] - ratio * this.arr[start_row][col];
            }
            this.target[row] -= ratio * this.target[start_row];
        }
    }

    public void full_reduce(){
        for (int i=0; i<this.size; i++){
            reduce(i, i);
        }
    }

    public double[] solve(){
        this.full_reduce();

        double[] X = new double[this.size];
        for (int i=this.size-1; i>=0; i--){
            double sum=0.0;
            for (int j = i+1; j<this.size; j++){
                sum += this.arr[i][j]*X[j];
            }
            X[i] = (this.target[i] - sum) / this.arr[i][i];
        }
        return X;
    }

    public String toString(){
        String result = "";
        for (int i=0; i<this.size; i++){
            for (int j=0; j<this.size; j++){
                result = result + this.arr[i][j] + " ";
            }
            result = result + "\n";
        }
        return result;
    }

    public static void main(String[] args){
        Matrix m = new Matrix(3);
        double[] w = new double[]{1,2,1,2,-1,1,3,0,2};
        double[] b = new double[]{8,3,9};
        for (int i=0; i<3;i++){
            for (int j=0; j<3; j++){
                m.set_matrix_element(i, j ,w[i*m.size+j]);
            }
        }
        System.out.println(m);

        for (int i=0; i<3; i++){
            m.set_target_element(i, b[i]);
        }

        double[] x = m.solve();
        for (int i=0; i<x.length; i++){
            System.out.print(x[i] + " ");
        }
        System.out.println();
        System.out.println(m);
    }


}

