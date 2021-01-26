# NEXT-Test
 8-queens puzzle.

public class EightQueens
    {
        //定義一個max表示共有多少個皇后
        static int _max = 8;

        //定義陣列arr,儲存皇后放置位置的結果，比如 arr={0,4,7,5,2,6,1,3}
        static int[] _arr = new int[_max];

        //初始化解法次數
        static int _count = 0;

        //初始化衝突次數
        static int _judgeCount = 0;
        public static void Test()
        {
            EightQueens.Check(0);

            Console.WriteLine($"一共有{_count}種解法");

            Console.WriteLine($"一共判斷衝突的次數{_judgeCount}次");
        }

        /// <summary>
        ///編寫一個方法，放置第n個皇后
        ///Check是每一次遞迴時，進入到Check中都有for(int i=0;i<_max;i++)，因此會有回溯
        /// </summary>
        /// <param name="n"></param>
        private static void Check(int n)
        {
            if (n == _max) //當n=8,說明8個皇后已經方法，因為初始值從0開始
            {
                Print();

                return;
            }

            //依次放入皇后，並判斷是否有衝突
            for (int i = 0; i < _max; i++)
            {
                //先把當前這個皇后n,放到該行的第1列
                _arr[n] = i;

                //判斷當放置第n個皇后到i列時，是否衝突
                if (Judge(n))
                {
                    //如果不衝突，接著放n+1個皇后，即開始遞迴
                    Check(n + 1);
                }

                //如果衝突，就繼續執行arr[n]=i,即將第n個皇后，放置在本行的後移的一個位置
            }
        }

        /// <summary>
        /// 檢視當我們放置第n個皇后，就去檢查該皇后是否和前面已經判斷的皇后衝突
        /// </summary>
        /// <param name="n">表示第n個皇后</param>
        /// <returns></returns>
        private static bool Judge(int n)
        {
            _judgeCount++;

            for (int i = 0; i < n; i++)
            {
                //1._arr[i] == _arr[n] 表示判斷第n個皇后，是否和前面的n-1個皇后在同一列
                //2.Math.Abs(n - i) == Math.Abs(_arr[n] - _arr[i])表示判斷第n個皇后是否和第i個皇后在同一個斜線
                //取個例子：當 n=1的時候 也就是放置第2列 Math.Abs(1-0)==Math.Abs(1-0)=1
                //3.判斷是否在同一行，沒有必要，n每次都在遞增
                if (_arr[i] == _arr[n] || Math.Abs(n - i) == Math.Abs(_arr[n] - _arr[i]))
                {
                    return false;
                }
            }

            return true;
        }

        /// <summary>
        /// 皇后的擺放位置輸出
        /// </summary>
        private static void Print()
        {
            _count++;

            for (int i = 0; i < _arr.Length; i++)
            {
                System.Console.Write(_arr[i] + " ");
            }

            System.Console.WriteLine();
        }
    }
