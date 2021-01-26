# NEXT-Test
//8-queens puzzle.

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

        private static void Check(int n)
        {
            if (n == _max) //當n=8,說明8個皇后已經方法，因為初始值從0開始
            {
                Print();

                return;
            }

            
            for (int i = 0; i < _max; i++)
            {
               
                _arr[n] = i;

               
                if (Judge(n))
                {
                 
                    Check(n + 1);
                }
            }
        }

        private static bool Judge(int n)
        {
            _judgeCount++;

            for (int i = 0; i < n; i++)
            {
                if (_arr[i] == _arr[n] || Math.Abs(n - i) == Math.Abs(_arr[n] - _arr[i]))
                {
                    return false;
                }
            }

            return true;
        }

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
