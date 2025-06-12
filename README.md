//zadanie 2
square :: Num a => a -> a
square x = x * x

cube :: Num a => a -> a
cube x = x * x * x

average :: Fractional a => a -> a -> a
average x y = (x + y) / 2

//zadanie3
quadraticRoots1 :: (Floating a, Ord a) => a -> a -> a -> String
quadraticRoots1 a b c =
  let d = b * b - 4 * a * c in
  if d < 0 then "Brak pierwiastków rzeczywistych"
  else if d == 0 then "x = " ++ show (-b / (2 * a))
  else
    let x1 = (-b + sqrt d) / (2 * a)
        x2 = (-b - sqrt d) / (2 * a)
    in "x1 = " ++ show x1 ++ ", x2 = " ++ show x2

quadraticRoots2 :: (Floating a, Ord a) => a -> a -> a -> String
quadraticRoots2 a b c
  | d < 0     = "Brak pierwiastków rzeczywistych"
  | d == 0    = "x = " ++ show (-b / (2 * a))
  | otherwise = "x1 = " ++ show x1 ++ ", x2 = " ++ show x2
  where
    d  = b * b - 4 * a * c
    x1 = (-b + sqrt d) / (2 * a)
    x2 = (-b - sqrt d) / (2 * a)

//zadanie4
factorial :: (Integral a) => a -> a
factorial 0 = 1
factorial n = n * factorial (n - 1)

//zadanie5
fibonacci :: (Integral a) => a -> a
fibonacci 0 = 0
fibonacci 1 = 1
fibonacci n = fibonacci (n - 1) + fibonacci (n - 2)

//zadanie6
minmax :: (Ord a, Num a) => a -> a -> a -> a
minmax a b c = maximum [a, b, c] - minimum [a, b, c]

//zadanie7
sumOfSquares :: Num a => a -> a -> a
sumOfSquares x y = x * x + y * y

//zadanie8
lastDigit :: Integral a => a -> a
lastDigit n = abs n `mod` 10


--1
rev :: [a] -> [a]
rev x = rev' x []

rev' :: [a] -> [a] -> [a]
rev' [] y = y
rev' (first:rest) y = rev' rest (first:y) 

--2
fun :: [(Int, Int, Int)] 
fun = [(x, y, x * y) | x<-[1..12], y<-[1..12]]

--3
colors = ["black", "white", "blue", "yellow", "red"]
colfn :: [String] -> [(String, String)]
colfn [x] = []
colfn (first:rest) = [(first, x) | x <- rest] ++ colfn rest 


--6
-- a) append
append :: [a] -> [a] -> [a]
append [] ys = ys
append (x:xs) ys = x : append xs ys

-- b) member
member :: Eq a => a -> [a] -> Bool
member _ [] = False
member x (y:ys)
  | x == y    = True
  | otherwise = member x ys

-- c) last
lastElem :: [a] -> a
lastElem [x] = x
lastElem (_:xs) = lastElem xs
lastElem [] = error "Pusta lista"

-- d) delete
deleteElem :: Eq a => a -> [a] -> [a]
deleteElem _ [] = []
deleteElem x (y:ys)
  | x == y    = ys
  | otherwise = y : deleteElem x ys

-- e) split
split :: Ord a => a -> [a] -> ([a], [a])
split _ [] = ([], [])
split x (y:ys)
  | y < x     = (y:l1, l2)
  | y > x     = (l1, y:l2)
  | otherwise = (l1, l2)
  where (l1, l2) = split x ys


--7
myFilter :: (a -> Bool) -> [a] -> [a]
myFilter _ [] = []
myFilter p (x:xs)
  | p x       = x : myFilter p xs
  | otherwise = myFilter p xs

-- Typ:
-- myFilter :: (a -> Bool) -> [a] -> [a]

--8
onlyEven :: [Int] -> [Int]
onlyEven = filter even

--9
doubleAll :: [Int] -> [Int]
doubleAll = map (*2)

--10
sumOfDigits :: Int -> Int
sumOfDigits n = sum $ map (read . (:[])) $ show $ abs n




--prolog
% Допустимые цвета
color(zielony).
color(czerwony).
color(niebieski).

% Главная процедура раскраски
color_graph(Graph, Coloring) :-
    assign_colors(Graph, Coloring),
    check_constraints(Graph, Coloring).

% Назначение цвета каждому узлу
assign_colors([], []).
assign_colors([Node|Rest], [Node-Color|ColoredRest]) :-
    color(Color),
    assign_colors(Rest, ColoredRest).

% Проверка, что никакие соседние узлы не имеют одинаковый цвет
check_constraints([], _).
check_constraints([Node-Neighbors|Rest], Coloring) :-
    member(Node-Color, Coloring),
    check_neighbors(Neighbors, Color, Coloring),
    check_constraints(Rest, Coloring).

check_neighbors([], _, _).
check_neighbors([Neighbor|Rest], Color, Coloring) :-
    member(Neighbor-NeighborColor, Coloring),
    Color \= NeighborColor,
    check_neighbors(Rest, Color, Coloring).




example_graph([
    a-[b, c],
    b-[a, c],
    c-[a, b]
]).

example_graph(G), color_graph(G, Coloring).




--concat
concatWithSpace :: String -> String -> String
concatWithSpace s1 s2 = s1 ++ " " ++ s2






--graph
% Определяем допустимые цвета
color(zielony).
color(niebieski).
color(czerwony).

% Определяем рёбра графа
edge(a, c).
edge(a, b).
edge(c, b).
edge(b, d).
edge(d, e).

% Симметричность рёбер (граф неориентированный)
edge(X, Y) :- edge(Y, X).

% Главный предикат — раскраска
coloring([
    a-ColorA,
    b-ColorB,
    c-ColorC,
    d-ColorD,
    e-ColorE
]) :-
    color(ColorA),
    color(ColorB),
    color(ColorC),
    color(ColorD),
    color(ColorE),

    % Ограничения: соседние вершины — разные цвета
    \+ (edge(a, b), ColorA = ColorB),
    \+ (edge(a, c), ColorA = ColorC),
    \+ (edge(b, c), ColorB = ColorC),
    \+ (edge(b, d), ColorB = ColorD),
    \+ (edge(d, e), ColorD = ColorE).





