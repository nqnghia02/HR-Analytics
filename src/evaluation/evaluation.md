\section*{Nhận Xét Kết Quả Trên Tập Test}

\section{I. Bảng Tổng Hợp Các Metric Trên Tập Test}

\begin{table}[H]
\centering
\begin{tabular}{|l|c|c|c|c|c|c|}
\hline
\textbf{Metric} & \textbf{Logistic} & \textbf{Random Forest} & \textbf{SVM} & \textbf{XGBoost} & \textbf{LightGBM} & \textbf{CatBoost} \\
\hline
Support (Attrition) & 39 & 39 & 39 & 39 & 39 & 39 \\
\hline
Precision (Attrition) & 0.340 & 0.419 & 0.429 & 0.273 & 0.242 & 0.301 \\
\hline
Recall (Attrition) & 0.462 & 0.333 & 0.154 & 0.615 & 0.564 & 0.641 \\
\hline
F1-Score & 0.391 & 0.371 & 0.226 & 0.378 & 0.338 & 0.410 \\
\hline
AUC-ROC & 0.741 & 0.728 & 0.734 & 0.756 & 0.709 & 0.712 \\
\hline
\end{tabular}
\caption{So sánh các mô hình trên tập test}
\end{table}

\section{II. Đánh Giá Từng Mô Hình}

\subsection{1. Logistic Regression}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item ROC AUC = 0.741: khả năng phân biệt tương đối giữa hai lớp.
    \item F1-score = 0.391: sự cân bằng giữa Precision và Recall chưa tốt.
    \item Precision = 0.340: chỉ 34\% dự đoán "Attrition" là đúng.
    \item Recall = 0.462: phát hiện được 46.2\% trường hợp thực tế.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Đường cong nằm trên đường chéo ngẫu nhiên, chưa lý tưởng (AUC > 0.9 mới tốt).
    \item Precision-Recall Curve: Giảm mạnh precision khi tăng recall, phản ánh đánh đổi rõ rệt.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item Mô hình phù hợp cho sàng lọc ban đầu.
    \item Cần cải thiện Recall nếu mục tiêu là phát hiện sớm Attrition.
\end{itemize}

\subsection{2. Random Forest}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item ROC AUC = 0.728: kém hơn Logistic Regression.
    \item F1-score = 0.371: chưa cải thiện đáng kể so với Logistic.
    \item Precision = 0.419, Recall = 0.333: nhiều trường hợp bị bỏ sót.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Gần với đường chéo ngẫu nhiên.
    \item Precision-Recall Curve: Precision giảm nhanh khi tăng recall.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item Random Forest không vượt trội so với Logistic Regression trong bài toán này.
\end{itemize}

\subsection{3. Support Vector Machine (SVM)}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item ROC AUC = 0.734: tương đương Logistic, nhưng không vượt trội.
    \item F1-score = 0.226: thấp nhất trong các mô hình.
    \item Precision = 0.429, Recall = 0.154: bỏ sót nhiều Attrition.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Đường cong không gần góc trên bên trái.
    \item Precision-Recall Curve: Precision cao nhưng Recall rất thấp.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item SVM kém hiệu quả trong bài toán này, đặc biệt về khả năng phát hiện Attrition.
\end{itemize}

\subsection{4. XGBoost}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item ROC AUC = 0.756: cao nhất trong các mô hình.
    \item F1-score = 0.378: cao hơn SVM và Random Forest.
    \item Precision = 0.273, Recall = 0.615: phát hiện tốt nhưng nhiều cảnh báo sai.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Đường cong vượt trội các mô hình khác.
    \item Precision-Recall Curve: Precision giảm mạnh khi tăng Recall.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item Ưu điểm: Recall và AUC cao, phù hợp nếu ưu tiên phát hiện sớm.
    \item Hạn chế: Precision thấp, nhiều cảnh báo sai.
\end{itemize}

\subsection{5. LightGBM}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item ROC AUC = 0.709: thấp hơn nhiều so với XGBoost và Logistic.
    \item F1-score = 0.338: chưa cân bằng giữa Precision và Recall.
    \item Precision = 0.242, Recall = 0.564: chấp nhận nhiều sai sót để đạt Recall.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Đường cong gần đường chéo ngẫu nhiên.
    \item Precision-Recall Curve: Precision thấp dù Recall trung bình.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item Ưu điểm: Recall tương đối cao.
    \item Hạn chế: Precision thấp, AUC thấp nhất trong các mô hình.
\end{itemize}

\subsection{6. CatBoost}

\subsubsection*{a. Đánh giá}
\begin{itemize}
    \item F1-score = 0.410: cao nhất trong tất cả các mô hình.
    \item Recall = 0.641: tốt nhất trong các mô hình.
    \item Precision = 0.301: chấp nhận được trong bối cảnh ưu tiên Recall.
    \item ROC AUC = 0.712: chưa vượt qua XGBoost nhưng vẫn ổn.
\end{itemize}

\subsubsection*{b. Biểu đồ}
\begin{itemize}
    \item ROC Curve: Tốt hơn ngẫu nhiên, nhưng chưa lý tưởng.
    \item Precision-Recall Curve: Giữ được Recall cao mà Precision không quá thấp.
\end{itemize}

\subsubsection*{c. Kết luận}
\begin{itemize}
    \item CatBoost là mô hình phù hợp nhất khi mục tiêu là phát hiện sớm nhân viên nghỉ việc.
    \item Chấp nhận một số cảnh báo sai để có Recall cao.
\end{itemize}
