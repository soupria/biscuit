[shark](../index.md) / [shark](./index.md)

## Package shark

### Types

| Name | Summary |
|---|---|
| [ApplicationLeak](-application-leak/index.md) | `data class ApplicationLeak : `[`Leak`](-leak/index.md)<br>A leak found by [HeapAnalyzer](-heap-analyzer/index.md) in your application. |
| [AppSingletonInspector](-app-singleton-inspector/index.md) | `class AppSingletonInspector : `[`ObjectInspector`](-object-inspector/index.md)<br>Inspector that automatically marks instances of the provided class names as not leaking because they're app wide singletons. |
| [FilteringLeakingObjectFinder](-filtering-leaking-object-finder/index.md) | `class FilteringLeakingObjectFinder : `[`LeakingObjectFinder`](-leaking-object-finder/index.md)<br>Finds the objects that are leaking by scanning all objects in the heap dump and delegating the decision to a list of [FilteringLeakingObjectFinder.LeakingObjectFilter](-filtering-leaking-object-finder/-leaking-object-filter/index.md) |
| [HeapAnalysis](-heap-analysis/index.md) | `sealed class HeapAnalysis : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html)<br>The result of an analysis performed by [HeapAnalyzer](-heap-analyzer/index.md), either a [HeapAnalysisSuccess](-heap-analysis-success/index.md) or a [HeapAnalysisFailure](-heap-analysis-failure/index.md). This class is serializable however there are no guarantees of forward compatibility. |
| [HeapAnalysisFailure](-heap-analysis-failure/index.md) | `data class HeapAnalysisFailure : `[`HeapAnalysis`](-heap-analysis/index.md)<br>The analysis performed by [HeapAnalyzer](-heap-analyzer/index.md) did not complete successfully. |
| [HeapAnalysisSuccess](-heap-analysis-success/index.md) | `data class HeapAnalysisSuccess : `[`HeapAnalysis`](-heap-analysis/index.md)<br>The result of a successful heap analysis performed by [HeapAnalyzer](-heap-analyzer/index.md). |
| [HeapAnalyzer](-heap-analyzer/index.md) | `class HeapAnalyzer`<br>Analyzes heap dumps to look for leaks. |
| [IgnoredReferenceMatcher](-ignored-reference-matcher/index.md) | `class IgnoredReferenceMatcher : `[`ReferenceMatcher`](-reference-matcher/index.md)<br>[IgnoredReferenceMatcher](-ignored-reference-matcher/index.md) should be used to match references that cannot ever create leaks. The shortest path finder will never go through matching references. |
| [KeyedWeakReferenceFinder](-keyed-weak-reference-finder/index.md) | `object KeyedWeakReferenceFinder : `[`LeakingObjectFinder`](-leaking-object-finder/index.md)<br>Finds all objects tracked by a KeyedWeakReference, ie all objects that were passed to ObjectWatcher.watch. |
| [Leak](-leak/index.md) | `sealed class Leak : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html)<br>A leak found by [HeapAnalyzer](-heap-analyzer/index.md), either an [ApplicationLeak](-application-leak/index.md) or a [LibraryLeak](-library-leak/index.md). |
| [LeakingObjectFinder](-leaking-object-finder/index.md) | `interface LeakingObjectFinder` |
| [LeakTrace](-leak-trace/index.md) | `data class LeakTrace : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html)<br>The best strong reference path from a GC root to the leaking object. "Best" here means the shortest prioritized path. A large number of distinct paths can generally be found leading to a leaking object. Shark prioritizes paths that don't go through known [LibraryLeakReferenceMatcher](-library-leak-reference-matcher/index.md) (because those are known to create leaks so it's more interesting to find other paths causing leaks), then it prioritize paths that don't go through java local gc roots (because those are harder to reason about). Taking those priorities into account, finding the shortest path means there are less [LeakTraceReference](-leak-trace-reference/index.md) that can be suspected to cause the leak. |
| [LeakTraceObject](-leak-trace-object/index.md) | `data class LeakTraceObject : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html) |
| [LeakTraceReference](-leak-trace-reference/index.md) | `data class LeakTraceReference : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html)<br>A [LeakTraceReference](-leak-trace-reference/index.md) represents and origin [LeakTraceObject](-leak-trace-object/index.md) and either a reference from that object to the [LeakTraceObject](-leak-trace-object/index.md) in the next [LeakTraceReference](-leak-trace-reference/index.md) in [LeakTrace.referencePath](-leak-trace/reference-path.md), or to [LeakTrace.leakingObject](-leak-trace/leaking-object.md) if this is the last [LeakTraceReference](-leak-trace-reference/index.md) in [LeakTrace.referencePath](-leak-trace/reference-path.md). |
| [LibraryLeak](-library-leak/index.md) | `data class LibraryLeak : `[`Leak`](-leak/index.md)<br>A leak found by [HeapAnalyzer](-heap-analyzer/index.md), where the only path to the leaking object required going through a reference matched by [pattern](-library-leak/pattern.md), as provided to a [LibraryLeakReferenceMatcher](-library-leak-reference-matcher/index.md) instance. This is a known leak in library code that is beyond your control. |
| [LibraryLeakReferenceMatcher](-library-leak-reference-matcher/index.md) | `data class LibraryLeakReferenceMatcher : `[`ReferenceMatcher`](-reference-matcher/index.md)<br>[LibraryLeakReferenceMatcher](-library-leak-reference-matcher/index.md) should be used to match references in library code that are known to create leaks and are beyond your control. The shortest path finder will only go through matching references after it has exhausted references that don't match, prioritizing finding an application leak over a known library leak. Library leaks will be reported as [LibraryLeak](-library-leak/index.md) instead of [ApplicationLeak](-application-leak/index.md). |
| [MetadataExtractor](-metadata-extractor/index.md) | `interface MetadataExtractor` |
| [ObjectInspector](-object-inspector/index.md) | `interface ObjectInspector` |
| [ObjectInspectors](-object-inspectors/index.md) | `enum class ObjectInspectors : `[`ObjectInspector`](-object-inspector/index.md)<br>A set of default [ObjectInspector](-object-inspector/index.md)s that knows about common JDK objects. |
| [ObjectReporter](-object-reporter/index.md) | `class ObjectReporter`<br>Enables [ObjectInspector](-object-inspector/index.md) implementations to provide insights on [heapObject](-object-reporter/heap-object.md), which is an object (class, instance or array) found in the heap. |
| [OnAnalysisProgressListener](-on-analysis-progress-listener/index.md) | `interface OnAnalysisProgressListener` |
| [ReferenceMatcher](-reference-matcher/index.md) | `sealed class ReferenceMatcher`<br>Used to pattern match known patterns of references in the heap, either to ignore them ([IgnoredReferenceMatcher](-ignored-reference-matcher/index.md)) or to mark them as library leaks ([LibraryLeakReferenceMatcher](-library-leak-reference-matcher/index.md)). |
| [ReferencePattern](-reference-pattern/index.md) | `sealed class ReferencePattern : `[`Serializable`](https://docs.oracle.com/javase/6/docs/api/java/io/Serializable.html)<br>A pattern that will match references for a given [ReferenceMatcher](-reference-matcher/index.md). |

### Exceptions

| Name | Summary |
|---|---|
| [HeapAnalysisException](-heap-analysis-exception/index.md) | `class HeapAnalysisException : `[`RuntimeException`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-runtime-exception/index.html) |

### Functions

| Name | Summary |
|---|---|
| [&lt;no name provided&gt;](-no name provided-.md) | `fun <no name provided>(): `[`Unit`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-unit/index.html)<br>Finds the objects that are leaking, for which Shark will compute leak traces. |
