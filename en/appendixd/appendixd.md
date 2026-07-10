# Appendix D

# Gonzo Example Applications

This Appendix contains the Lisp code used in Gonzo to produce the examples described in Chapter 7, Section 7.3. The code used in Geco to produce online visualizations is given in section D.1. The code used in Gonzo to produce the oine visualizations of the maximum integer problem, the De Jong F1 test problem, and the royal road function, are given in Section D.2.

# D.1 Online Visualization

The following annotated version of the Geco EVOLVE method is used to produce online visualizations in Gonzo. The annotataions made to the original Geco EVOLVE method are shown here in bold.

(defmethod EVOLVE ((self ecosystem)) (unless viz::\*visualization-dialog\* (viz::create-visualizations self )) (evaluate self (plan self)) (mapcar #'(lambda (view) (setf (current-generation-range view) (mapcar #'incf (current-generation-range view))) (setf (total-generation-range view) (list (rst (total-generation-range view)) (incf (second (total-generation-range view)))))

(cond ((or ( $<$ (min-score (elt 0 (statistics (plan self )))) (rst (total-tness-range view))) ( $>$ (max-score (elt 0 (statistics (plan self )))) (second (total-tness-range view)))) (setf (total-tness-range view) (list (min (min-score (elt 0 (statistics (plan self )))) (rst (total-tness-range view))) (max (max-score (elt 0 (statistics (plan self )))) (second (total-tness-range view))))))) (viz::views viz::\*visualization-dialog\*)))   
(unless (evolution-termination-p (plan self))   
(incf (generation-number self))   
(regenerate (plan self) self)   
(evolve self)))

# D.2 Gonzo Example Problem Visualizations

This section presents the code used in Gonzo to produce the three example problem visualizations presented in Section 7.4.

# D.2.1 The Maximum Integer Problem

The following Lisp code was used to produce the Gonzo visualization shown in Figure 7.9 of the maximum integer problem, see page 199.

(defvar \*visualization-dialog\* nil) ;; visualization container dialog

(defun maxint ()

(test-plan 'run-1 1 'maxint-plan) ;; Geco GA dataset run-1 (create-visualizations run-1) ;; Gonzo create visualizations function

) ;; test

(defmethod create-visualizations ((run ecosystem)) (setf \*visualization-dialog\* (open-dialog nil ;; list-of-dialog-items 'my-navigator ;; device cg:\*screen\* ;; stream :name 'visualizer ;; name :pop-up-p nil ;; not a pop-up dialog :background-color cg::white ;; background colour :window-exterior (cg:make-box 30 50 1030 850) ;; window exterior box :title "Test")) ;; title string for window

(create-fitness-versus-time-graph 'fitness-graph-0 ;; name run ;; dataset \*visualization-dialog\* ;; parent-dialog (cg:make-box 400 600 1000 800)) ;; exterior-box (create-fine-grained-chromosome-view 'text-view-0 ;; name \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 350 400 800)) ;; exterior-box (create-search-space-visualization 'scatterplot-view-0 ;; name run ;; dataset

'GSM-D-circle ;; chromosome-mapping-technique \*visualization-dialog\* ;; parent-dialog (cg:make-box 400 0 1000 600) ;; exterior-box 'D-GSM ;; coordinate-mapping-technique (list text-view-0)) ;; list-of-views

(create-generation-fitness-selector 'view-range-window ;; name (list scatterplot-view-0) ;; list-of-views \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 85 400 250)) ;; exterior-box (create-schema-highlight-selector 'schema-editor-window ;; name (list scatterplot-view-0) ;; list-of-views \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 250 400 350)) ;; exterior-box

) ;; create-visualizations

# D.2.2 The De Jong F1 Test Problem

The followingcode was used to produce the example visualizations of a GA solving De Jong's F1 test problem, as shon in Figure 7.12, see page 202. This code is virtually identical to that used to produce the visualizations of the maximum integer problem given in the previous subsection, the only dierences being a change in the GA's genetic plan, the image mapping used in the search space visualization, and the window dimensions of the schema highlight selector and ne grained chromosome view.

(defvar \*visualization-dialog\* nil) ;; visualization container dialog

(defun dejong () (test-plan 'run-1 1 'dejong-plan) ;; Geco GA dataset run-1 (create-visualizations run-1) ;; Gonzo create visualizations function   
) ;; test

(defmethod create-visualizations ((run ecosystem)) (setf \*visualization-dialog\* (open-dialog nil ;; list-of-dialog-items 'my-navigator ;; device cg:\*screen\* ;; stream :name 'visualizer ;; name :pop-up-p nil ;; not a pop-up dialog :background-color cg::white ;; background colour :window-exterior (cg:make-box 30 50 1030 850) ;; window exterior bo :title "Test")) ;; title string for window

(create-fitness-versus-time-graph 'fitness-graph-0 ;; name run ;; dataset \*visualization-dialog\* ;; parent-dialog (cg:make-box 400 600 1000 800)) ;; exterior-box (create-fine-grained-chromosome-view 'text-view-0 ;; name \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 430 400 800)) ;; exterior-box (create-movie-player 'control-panel ;; name '(i< << <1 > 1> >> >i) ;; list-of-lables '(start rewind back1 play-pause forward1 fforward end) ;; list-of-functions (list scatterplot-view-0) ;; list-of-views \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 0 400 85)) ;; exterior-box

(create-generation-fitness-selector 'view-range-window ;; name (list scatterplot-view-0) ;; list-of-views \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 85 400 250)) ;; exterior-box (create-schema-highlight-selector 'schema-editor-window ;; name (list scatterplot-view-0) ;; list-of-views \*visualization-dialog\* ;; parent-dialog (cg:make-box 0 250 400 430)) ;; exterior-box

) ;; create-visualizations

# D.2.3 The Royal Road Problem

The royal road problem was the last example presented in Section 7.4. In order to produce this visualization, a new method was created to generate matrices of search space visualizations. This create-search-space-visualization-matrix method is presented here along with the code used to produce the example visualization of a GA solving the royal road problem.

(defmethod create-search-space-visualization-matrix (name-list (dataset ecosystem) chromosome-mapping-technique parent-dialog list-of-exterior-boxes coordinate-mapping-technique list-of-list-of-views list-of-projection-locus-orderings )

(mapcar #'(lambda (name exterior-box list-of-views loci-list)

dataset   
chromosome-mapping-technique   
parent-dialog   
exterior-box   
coordinate-mapping-technique   
list-of-views   
loci-list))

name-list window-boxes list-of-list-of-views list-of-projection-locus-orderings )

) ;; create-search-space-visualization-matrix

This create-search-space-visualization-matrix method was applied as follows to produce the visualization shown in Figure 7.14, see page 205.

(create-search-space-visualization-matrix '(scatterplot-view-0 scatterplot-view-1 scatterplot-view-2 scatterplot-view-3 scatterplot-view-4 scatterplot-view-5 scatterplot-view-6 scatterplot-view-7) ;; list-of-names

run-1 ;; dataset

'GSM-D-circle ;; chromosome-mapping-technique \*visualization-dialog\* ;; parent-dialog

'D-GSM ;; coordinate-mapping-technique (list text-view-0) ;; list-of-views

\`((0 1 2 3 4 5 6 7) (8 9 10 11 12 13 14 15) (16 17 18 19 20 21 22 23)

(24 25 26 27 28 29 30 31) (32 33 34 35 36 37 38 39) (40 41 42 43 44 45 46 47)

(48 49 50 51 52 53 54 55) (56 57 58 59 60 61 62 63))) ;; list-of-pro jection-locus-orderings